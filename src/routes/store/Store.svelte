<script>
	import { onMount } from 'svelte';
	/**
	 * @type {any[]}
	 */
	let products = [];

	onMount(async () => {
		products = await getProducts();
	});

	async function getProducts() {
		const res = await fetch('https://fakestoreapi.com/products');
		const products = await res.json();
		console.log(products);

		if (res.ok) {
			return products;
		} else {
			throw new Error('Something went wrong!');
		}
	}
</script>

{#each products as product}
	<div>
		<h3>{product.id}.{product.title}</h3>
		<div>
			<img src={product.image} alt="images" />
		</div>
	</div>
{/each}
