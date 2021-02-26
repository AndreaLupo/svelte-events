<script>
	import {tick} from 'svelte';
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

	let text ='This is some dummy text';

	function addToCard(event) {
		console.log(event.detail);
	}

	function deleteProduct(event) {
		console.log(event.detail);
	}

	function transform(event) {
		if(event.which !== 9) {
			// different from `Tab` key
			return;
		}
		event.preventDefault();

		const selectionStart = event.target.selectionStart;
		const selectionEnd = event.target.selectionEnd;
		const value = event.target.value;

		text = value.slice(0, selectionStart) + value.slice(selectionStart, selectionEnd).toUpperCase() + value.slice(selectionEnd);
	
		tick().then(() => {
			event.target.selectionStart = selectionStart;
			event.target.selectionEnd = selectionEnd;
		}); 
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

<textarea  rows="5" value={text} on:keydown={transform}></textarea>