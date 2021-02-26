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

	let showModal = false;
	let closable = false;

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

<button on:click="{() => showModal = true}">Show modal</button>

{#if showModal}
	<Modal on:close="{()=> showModal = false}" on:cancel="{()=> showModal = false}"
		let:didAgree={closable}>
		<h1 slot="header">Hello!</h1>	
		<p>This works!</p>
		<button slot="footer" on:click="{()=> showModal = false}"
			disabled={!closable}
			>Confirm
		</button>
	</Modal>
{/if}