<script>
	import Product from "./Product.svelte";
	import Modal from "./Modal.svelte";

	let products = [
        {
            id: 'p1',
            title: 'Title',
            price: 9.99
        }
    ];


	function addToCard(event) {
		console.log(event.detail);
	}

	function deleteProduct(event) {
		console.log(event.detail);
	}


</script>
{#each products as product}
	<Product {...product} 
		on:add-to-cart="{addToCard}"
		on:delete="{deleteProduct}"/>
{/each}

<Modal>
	<h1>
		Hello!
	</h1>	
	<p>This works!</p>
</Modal>