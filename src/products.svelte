<script>
	import {createEventDispatcher} from 'svelte';
	
	const dispatch = createEventDispatcher();
	
	export let currentCategory;
	export let products;
	export let drinks;
	export let pizzas;
	export let kebabs;
	export let burgers;
	export let sides;
	export let deserts;
	
	let items = {};
	let prices = ['3.00', '2.00', '1.00'];
	
	let selected = ['false', 'true', 'false'];
	
	let size = ['Large', 'Normal', 'Small'];
	
	let sizes = new Array(size.length).fill()
		.map((_, i) => {
			return {
				item: size[i % size.length],
				selection: selected[i % selected.length],
				price: prices[i % prices.length]
			};
		});
	
	if(currentCategory == 'Drinks'){ 
		products = new Array(drinks.length);
		products = drinks;
	}
	if(currentCategory == 'Pizza'){ 
		products = new Array(pizzas.length);
		products = pizzas;
	}
	if(currentCategory == 'Kebabs'){ 
		products = new Array(kebabs.length);
		products = kebabs;
	}
	if(currentCategory == 'Burgers'){ 
		products = new Array(burgers.length);
		products = burgers;
	}
	if(currentCategory == 'Side Orders'){ 
		products = new Array(sides.length);
		products = sides;
	}
	if(currentCategory == 'Deserts'){ 
		products = new Array(deserts.length);
		products = deserts;
	}
													

				
		
		
	function addTo(p){
		const product = {...p, qty: 1, sub: p.price, id: Math.random()};
		dispatch( 'addToCart', product);
	}
	function updateSize(s, p){
		const product = p;
		const size = s;
		dispatch( 'updateSize', {size, product});
	}
</script>
<style>
	.Products{
		display: block;
		width: 50%;
		border: 1px Solid #333;
		margin: 50px 8px;
		padding: 12px 8px;
		background: #c3c3c3;
		border-radius: 5px;
	}
	.Products h3{
		font-family: "Comic Sans MS";
		font-size: 16px;
		text-transform: uppercase;
		line-height: 6px;
		margin: 1px 0px;
	}
	.Products ul{
		text-align: left;
		list-style: none;
		margin: 15px -40px;
		width: 100%
	}
	.Products ul li{
		margin: 6px 2px;
		padding: 2px;
		border: 1px Solid #333;
		background: #f4f4f4;
		border-radius: 5px;
		box-shadow: 1px 2px 3px rgba(0,0,0,0.2);
	}
	.Products ul li span{
		font-size: 24px;
		text-transform: uppercase;
	}
	label{
		display: inline;
		font-size: 10px;
		margin: 2px;
	}
	button{
		margin: 5px 12px;
		font-family: "Comic Sans MS";
		font-size: 12px;
		text-transform: uppercase;
	}
	section{
		font-size: 14px;
		margin: 4px 2px;
	}
	.Price{
		width: 60px;
	}
</style>

<div class="Products">
	<h3>{currentCategory} Products</h3>

	<ul>
		{#each products as p}
			<li><span>{p.name}  
				<section>size:
	{#each sizes as s, i}	
	<label for={s.item}>{s.item}</label>
	<input type="radio" checked={s.item === p.size} on:click={updateSize(s.item, p)}>	
	{/each}
				</section></span>
					<p><b>Price:</b> <input class="Price" type="text" 

bind:value={p.price}><button on:click={addTo(p)}>Add</button></p>
				</li>
		{/each}
	</ul>

</div>