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

<h3 class="text-gray-600 text-2xl font-medium p-7">Products</h3>
<div class="grid gap-6 p-7 grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 mt-6">
	{#each products as product}
		<div
			class="transition duration-150 ease-out hover:ease-in w-full max-w-sm mx-auto rounded-md p-2 shadow-md overflow-hidden"
		>
			<div class="flex items-end justify-center h-60 w-60 bg-cover">
				<img src={product.image} alt="images" />
			</div>
			<button
				class="p-2 mb-5 float-right rounded-full bg-blue-600 text-white mx-5 hover:bg-blue-500 focus:outline-none focus:bg-blue-500"
			>
				<svg
					class="h-5 w-5"
					fill="none"
					stroke-linecap="round"
					stroke-linejoin="round"
					stroke-width="2"
					viewBox="0 0 24 24"
					stroke="currentColor"
					><path
						d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z"
					></path></svg
				>
			</button>

			<div class="px-5 py-3">
				<h3 class="text-gray-700 font-semibold uppercase">{product.title}</h3>
				<span class="text-gray-500 mt-5 font-semibold">${product.price}</span>
			</div>
		</div>
	{/each}
</div>
