<script>
	import {createEventDispatcher} from 'svelte';
	
	const dispatch = createEventDispatcher();
	export let menuItem;
	
</script>
<style>
	h3{
		display: block;
		position: relative;
		padding: 10px auto;
		font-family: "Cambria";
		text-transform: uppercase;
	}
	.Categories-Menu{
		display: block;
		position: relative;
		text-align: left;
	}
	.Categories-Menu ul{
		position: relative;
		float: left;
		margin: 48px -160px;
	}
	.Categories-Menu ul li{
		display: block;
		position: relative;
		border: 1px Solid #fff;
		border-radius: 8%;
		padding: 6px;
		margin: 0 10px;
		list-style: none;
		text-transform: uppercase;
		text-decoration: none;
		color: #333;
		background: orange;
		font-family: "Comic Sans MS";
		font-size: 14px;
		font-weight: 900;
	}
	.Categories-Menu ul li:hover{
		text-shadow: 2px 2px 5px #fff;
		box-shadow: 2px 2px 5px #f00;
		border: 1px Solid #333;
		cursor: pointer;
	}
	.Categories-Menu ul li div{
		color: #333;
	}
</style>

<h3>Categories</h3>
<nav class="Categories-Menu">
	<ul>
		{#each menuItem as m}
		<li>
			<div on:click={() =>dispatch( 'setCat', m.item)}>{m.item}</div>
		</li>
		{/each}
	</ul>
</nav>