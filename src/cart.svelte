<script>
	import {createEventDispatcher} from 'svelte';
	
	const dispatch = createEventDispatcher();
	export let selectedItems;
	export let total;
	
	function decrease(s){
		const product = s;
		dispatch('decreaseQTY', product);
	}
	function increase(s){
		const product = {...s};
		dispatch('increaseQTY', product);
	}
	function removeFrom(s){
		const product = s;
		dispatch('removeFromCart', product);
	}
</script>
<style>
	.Cart{
		display: block;
		width: 40%;
		border: 1px Solid #333;
		margin: 50px -6px;
		padding: 12px 8px;
		background: #c3c3c3;
		border-radius: 5px;
	}
	.Cart h3{
		font-family: "Comic Sans MS";
		font-size: 16px;
		text-transform: uppercase;
		line-height: 8px;
		margin: 1px 0px;
	}
	.Cart h2{
		font-family: "Comic Sans MS";
		font-size: 20px;
		font-weight: 900;
		text-transform: uppercase;
		line-height: 8px;
		margin: 10px 0px;
	}
	.Cart ul{
		text-align: left;
		list-style: none;
		margin: 12px -40px;
		width: 100%
	}
	.Cart ul li{
		margin: 6px 2px;
		padding: 1px 5px;
		border: 1px Solid #333;
		background: #f4f4f4;
		border-radius: 5px;
		box-shadow: 1px 2px 3px rgba(0,0,0,0.2);
	}
	.Cart ul li span{
		font-size: 24px;
		text-transform: uppercase;
		padding: 5px;
	}
	button{
		margin: 4px 6px;
		padding: 4px 6px;
		text-align: center;
	}
	.remove{
		margin: 5px 0;
		font-family: "Comic Sans MS";
		font-size: 10px;
		text-transform: uppercase;
	}
</style>

<div class="Cart">
	<h3>Shopping cart</h3>
{#if selectedItems.length === 0}
	<p>Your Shopping Cart is Empty :(</p>
{:else}
	<ul>
		{#each selectedItems as s}
		<li><span>{s.name}</span><br/><sub>Size: {s.size}</sub><br/> 
Qty: <button on:click={decrease(s)}>-</button>{s.qty}<button on:click={increase(s)}>+</button>
<br/>Sub-Total: <input type="text" style="width: 60px" bind:value={s.sub}><br/><button class="remove" on:click={removeFrom(s)}>Remove</button></li>
		{/each}
	</ul>
{/if}
	<h2><b>Total: {total}</b></h2>
<button on:click={() =>dispatch('checkOut', selectedItems)}>Checkout</button>
</div>