<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  import { scale} from 'svelte/transition';
  
  const closeDispatch = createEventDispatcher();
  
  const close = () => {
    closeDispatch('close-word-modal');
  }

  let aboutModalVisible = true;
  export let word: string;
  export let borderColor: string;
  $: year = 1900 + Math.floor(Math.random()*120);

</script>
<div>
  {#if aboutModalVisible}
  <div class="backdrop1" >
    <br class="normal" />  
    <div class="modal1" style="{'background-color:' + borderColor + ';'}"  transition:scale >
      <div class="row">
        <div class="col l2 m2 s2"></div>
        <div class="col l8 m8 s8">
          <h5>{word}<br /> ({year})</h5>
          </div>
        <div class="col l2 m2 s2">
          <span class="tooltipped btn btn-floating transparent waves-effect waves-light z-depth-1" data-tooltip="Click to close" on:click="{close}">
            <i class="fas fa-times-circle"></i>
          </span>
        </div>
      </div>
      <div class="row">
        <div class="modalbody">
          <hr />
            <p class="lorem">
              <img class="picsum" src="https://picsum.photos/seed/{year}/80/80" alt="{word}" title="{word}" width=80 height=80 />
              Lorem ipsum dolor sit amet consectetur adipisicing elit. Suscipit illo debitis, explicabo cumque eaque alias, quod consequatur totam vitae accusantium rem fuga animi tenetur est vero neque omnis pariatur quasi!
            </p>
            <hr />
            <button class="tooltipped btn-large z-depth-3 transparent darken-5 waves-effect waves-light" data-tooltip="Click to close" on:click="{close}"><i class="fas fa-times-circle"></i>&nbsp;Close</button>
        </div>
      </div>
    </div>
  </div>
{/if}
</div>

<style>
  .normal {
    line-height: 1rem;
  }
  .fa-times-circle {
    cursor: pointer;
    font-weight: 900;
    font-size: 2rem;
    vertical-align:middle;
  }
  .backdrop1 {
    top: 0px;
    left: 0px;
    width: 100%;
    height: 100%;
    position: fixed;
    background-color: rgba(0,0,0,.8);
    z-index: 100;
  }

  /* do not rename as 'modal' or it interferes with Materialize-CSS modals  */
  .modal1 {
    padding: 0.2rem 2rem .5rem 2rem;
    border-radius: 5rem .5rem 5rem 5rem;
    border-width: 10px;
    border-style: inset;
    max-width: 400px;
    margin: 5% auto;
    text-align: center;
    background-color: rgb(255, 255, 255);
    color: #fff;
    line-height: normal;
    z-index: 200;
  }
  h5 {
    font-weight:600;
  }
  p {
    font-weight:400;
    font-size: 1.25rem;
  }

  a {
    color: #1f1fff;
    text-decoration: none;
  }
  a:hover {
    color: #00a30e;
  }
  button {
    font-weight: 600;
    font-size: 1.5rem;
  }

  .lorem {
    float:none;
  }
  .picsum {
    border: 0 none;
    padding: 0;
    float:left;
    width: 80px;
    vertical-align:text-top;
    border-radius: 10px;
  }

</style>