<script>
	import Header from '$lib/header/Header.svelte';
	import '../app.css';
	import "carbon-components-svelte/css/g10.css";
</script>


<Header />

<main>
	<slot />
</main>

<svelte:head>
	<title>Auto Prestige</title>
	<meta name="description" content="Car dealership" />
</svelte:head>

<footer>

</footer>

<style>
	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		padding: 1rem;
		width: 100%;
		max-width: 2024px;
		margin: 0 auto;
		box-sizing: border-box;
		min-height: 800px;
		background-color: rgb(20, 20, 20);
	}

	footer {
		background-color: rgb(20, 20, 20);
	}
</style>
