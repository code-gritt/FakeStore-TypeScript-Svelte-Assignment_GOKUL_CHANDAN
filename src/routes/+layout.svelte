<script>
	import './styles.css';
	import Header from './Header.svelte';
	import Footer from './Footer.svelte';
</script>

<div class="app">
	<main>
		<Header />
		<slot />
		<Footer />
	</main>
</div>
