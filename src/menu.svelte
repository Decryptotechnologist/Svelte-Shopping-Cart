<script>
	let items = ['home', 'categories', 'products', 'cart'];
	
	let menuItems = new Array(4).fill()
		.map((_, i) => {
			return {
				item: items[i % items.length]
			};
		});
</script>
<style>
	.Menu{
		display: flex;
		position: relative;
		width: 100%;
		text-align: center;
	}
	.Menu ul{
		width: 100%;
	}
	.Menu ul li{
		display: inline;
		position: relative;
		border: 1px Solid #fff;
		border-radius: 8%;
		padding: 6px;
		margin: auto;
		list-style: none;
		text-transform: uppercase;
		text-decoration: none;
		color: #333;
		background: orange;
		font-family: "Comic Sans MS";
		font-size: 14px;
		font-weight: 900;
	}
	.Menu ul li:hover{
		text-shadow: 2px 2px 5px #fff;
		box-shadow: 2px 2px 5px #f00;
		border: 1px Solid #333;
		cursor: pointer;
	}
	.Menu ul li a{
		color: #333;
	}
</style>

<nav class="Menu">
	<ul>
		{#each menuItems as m}
			<li><a href="{m.item}.svelte">{m.item}</a></li>
		{/each}
	</ul>
</nav>