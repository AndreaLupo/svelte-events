<script>
	import Product from "./Product.svelte";

	function addToCard(event) {
		console.log(event.detail);
	}

	function deleteProduct(event) {
		console.log(event.detail);
	}


</script>

<Product productTitle="A Book" on:add-to-cart="{addToCard}"
	on:delete="{deleteProduct}"/>
