<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';
	import '../app.css';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>


<header class="sticky top-0 z-50 border-b-2 bg-white/80 backdrop-blur">
	<div class="mx-auto px-6">
		<nav class="flex gap-4 py-4">
			<h2> <a href="/">Favorite Dishes</a> </h2>
			<h2><a href="/adventures">Cooking Adventures</a></h2>
			<h2><a href="/about">About Me</a></h2>
		</nav>
	</div>
</header>

<main> 
	{@render children()}
</main>

