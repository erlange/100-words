<script lang="ts">
  import { scale} from 'svelte/transition';
  import WordComponent from './random-child.svelte';
  import WordModalComponent from './modal.word.svelte';
  import {generateName} from '../utils/random-names';

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

	let wordModalVisible = false;

  let theWords = generateNames(seed);

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