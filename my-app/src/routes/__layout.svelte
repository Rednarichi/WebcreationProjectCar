<script>
	import Header from '$lib/header/Header.svelte';
	import '../app.css';
</script>

<Header />

<main>
	<slot />
</main>

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
