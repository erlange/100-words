<script lang="ts">
	import {Route, Router, Link}from 'svelte-navigator';
	import RandomComponent from "./components/random.svelte";
	import AboutModalComponent from './components/modal.about.svelte';

	let randomInstance: RandomComponent;
	let title = '100-Words';
	let aboutModalVisible = false;

	const shuffle = () => {
		randomInstance.randomize(100);
	}
</script>
<svelte:head>
  <title>{title}</title>
</svelte:head>

<Router basepath="/100-words" primary={false}>
<div  class="row">
	<nav>
		<div class="nav-wrapper indigo">
			<!-- <a href="#!" class="brand-logo">Logo</a> -->
			<div class="col xl1 l1 m1"></div>
			<div class="col xl2 l2 m2"><Link class="hide-on-sm" to="/"><h5>100-Words</h5></Link></div>
			<div class="col xl8 l8 m8">
				{#if aboutModalVisible}
					<AboutModalComponent on:close-about-modal={() => aboutModalVisible = false}></AboutModalComponent>
				{/if}
				
				<ul class="right hide-on-sm">
					<li>
						<span class="z-depth-3 tooltipped btn-floating btn-large blue waves-effect waves-light" data-tooltip="Click to shuffle!" on:click="{shuffle}">
							<i class="fas fa-redo"></i>
						</span>&nbsp&nbsp&nbsp&nbsp
					</li>
					<li>
						<span class="z-depth-3 tooltipped btn-floating btn-large pink waves-effect waves-light darken-2" data-tooltip="About" on:click="{() => aboutModalVisible = true}">
							<i class="fas fa-question-circle" style="font-size:1.5rem;"></i>
						</span>
					</li>
					<li>
						<a href="https://github.com/erlange/100-words" class="z-depth-3 tooltipped btn-floating btn-large waves-effect waves-light green" data-tooltip="Go to Github page">
							<i class="fab fa-github" style="font-size:1.5rem;"></i>
						</a>
					</li>
				</ul>
		</div>
		<div class="col l1 m1"></div>
		</div>
	</nav>
</div>


<main class="row">
	<div class="col xl1 l1 m1 s0 xs0"></div>
		<div class="col xl10 l10 m10 s12 xs12">
			<Route path="/" primary={false}>
				<RandomComponent bind:this={randomInstance}></RandomComponent>
			</Route>
		<div class="col xl1 l1 m1 s0 xs0"></div>
	</div>
	</main>
</Router>

<style>
</style>