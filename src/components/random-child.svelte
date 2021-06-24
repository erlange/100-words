<script lang="ts">
  import { scale} from 'svelte/transition';
  import { bounceInOut} from 'svelte/easing';

  export let value: string;
  export let bgcolor: string;

</script>
{#key value}
    <div class="z-depth-2 word" style="{'background-color:' + bgcolor + ';'}" on:click transition:scale="{{delay: 200, duration: 200, easing: bounceInOut }}">
      { value }
    </div>
{/key}

<style>
  .word {
    float: left;
    background-color: #4b0082;
    font-weight: 700;
    color: #fff;
    padding: .6rem .6rem 1rem 1rem;
    cursor: pointer;
    margin: .2rem;
    border-radius: 2rem .5rem 2rem 2rem;
    box-shadow: 0 2px 2px 0 #00000024,0 3px 1px -2px #0000001f,0 1px 5px 0 #00000033;
    text-shadow: -2px -2px 2px rgba(130,130,130,0.81);
    font-size: 1.2rem;
  }

  div:hover {
    color: #ffff00;
  }

</style>