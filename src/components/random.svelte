<script lang="ts">
  import { scale, fade} from 'svelte/transition';
  import WordComponent from './random-child.svelte';
  import WordModalComponent from './modal.word.svelte';
  import {generateName} from './random-names.svelte';
import { onMount } from 'svelte';

  interface IWord {
    word: string;
    bgColor: string
  };

  const generateNames = (max: number = 10): IWord[] => {
    let words: IWord[] = [];
    let maxColor = 200;
    for (let i = 0; i < max; i++) {
      try {
        words.push({
          word: generateName(),
          bgColor: `rgb(${Math.floor(Math.random() * maxColor)}, ${Math.floor(Math.random() * maxColor)}, ${Math.floor(Math.random() * maxColor)})`
        });
      } 
      catch (error) {
        console.log(error);
      }
    }
    return words;
  }

  const replaceName = (value: number) => {
    theWords[value].word = generateName();
  } 

  export const randomize = (max: number = 10) => {
    theWords = generateNames(max);
  }

  let currentWord: IWord;
  export let seed: number = 100;

  const select = (index: number) => {
    currentWord = theWords[index];
    wordModalVisible = true;
  }

  const autoRandomize = (max: number = 25) => {
    const interval = setInterval(() => {
      const which = [] as number[];
      for (let i = 0; i < max; i++) {
        which.push(Math.floor(Math.random() * 100));
      }
      which.forEach(f => {
        theWords[f].word = generateName();
      });
    }, 5000);
    return () => {
      clearInterval(interval);
    };
  }

  onMount(() => {
    autoRandomize(10);
  });

	let wordModalVisible = false;

  let theWords = generateNames(seed);

  // autoRandomize(10);


</script>
  {#if wordModalVisible}
    <WordModalComponent word="{currentWord.word}" borderColor="{currentWord.bgColor}" on:close-word-modal={() => wordModalVisible = false} />
  {/if}

  <div class="outer">
    {#each theWords as word, index (index) }
      <div transition:scale>
        <WordComponent bind:value="{word.word}" bind:bgcolor="{word.bgColor}" on:click={() => select(index)} />
      </div>
  {/each}
</div>

<style>
</style>