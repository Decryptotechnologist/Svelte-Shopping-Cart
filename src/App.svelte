<script>
	import Header from './header.svelte';
	import Footer from './footer.svelte';
	import Categories from './categories.svelte';
	import Products from './products.svelte';
	import Cart from './cart.svelte';

	let currentCategory= 'Drinks';
	let items = ['Drinks', 'Pizza', 'Kebabs', 'Burgers', 'Side Orders', 'Deserts'];
	let products = [];
	
	let smallDrink = '1.00';
	let normalDrink = '2.00';
	let largeDrink = '3.00';
	
	let smallPizza = '10.00';
	let normalPizza = '12.00';
	let largePizza = '14.00';
	
	let smallKebab = '5.00';
	let normalKebab = '6.00';
	let largeKebab = '7.00';
	
	let smallBurger = '1.50';
	let normalBurger = '2.00';
	let largeBurger = '3.00';
	
	let smallSide = '1.00';
	let normalSide = '2.00';
	let largeSide = '3.00';
	
	let smallDesert = '2.00';
	let normalDesert = '4.00';
	let largeDesert = '6.00';
	
	let cartItems = [{name: 'Item 1', size: 'Normal', price: '1.00', qty: 1, sub: '1.00', id: Math.random(), type: 'Item'}, {name: 'Item 2', size: 'Normal', price: '1.00', qty: 1, sub: '1.00', id: Math.random(), type: 'Item'}];
	
	let prices = ['1.00', '2.00'];
	
	let total = parseFloat(prices[1]).toFixed(2);

	let selectedItems = new Array(cartItems.length).fill()
		.map((_, i) => {
			return {
				name: cartItems[i].name,
				size: cartItems[i].size,
				price: cartItems[i].price,
				qty: cartItems[i].qty,
				sub: cartItems[i].sub,
				id: cartItems[i].id,
				type: cartItems[i].type
			};
		});
	
	let menuItem = new Array(6).fill()
		.map((_, i) => {
			return {
				item: items[i % items.length]
			};
		});
	
	let drinks = [
		{name: 'Coke', size: 'Normal', price: normalDrink, id: Math.random(), type: 'Drink'},
		{name: 'Pepsi', size: 'Normal', price: normalDrink, id: Math.random(), type: 'Drink'},
		{name: '7Up', size: 'Normal', price: normalDrink, id: Math.random(), type: 'Drink'},
		{name: 'Sprite', size: 'Normal', price: normalDrink, id: Math.random(), type: 'Drink'},
		{name: 'Fanta', size: 'Normal', price: normalDrink, id: Math.random(), type: 'Drink'}];
	
	let pizzas = [
		{name: 'Cheese Feast', size: 'Normal', price: normalPizza, id: Math.random(), type: 'Pizza'},
		{name: 'Hawian', size: 'Normal', price: normalPizza, id: Math.random(), type: 'Pizza'},
		{name: 'Pepperoni', size: 'Normal', price: normalPizza, id: Math.random(), type: 'Pizza'},
		{name: 'Chicken Surprise', size: 'Normal', price: normalPizza, id: Math.random(), type: 'Pizza'},
		{name: 'Meat Feast', size: 'Normal', price: normalPizza, id: Math.random(), type: 'Pizza'}];
	
	let kebabs = [
		{name: 'Donner', size: 'Normal', price: normalKebab, id: Math.random(), type: 'Kebab'},
		{name: 'Chicken', size: 'Normal', price: normalKebab, id: Math.random(), type: 'Kebab'},
		{name: 'Shish', size: 'Normal', price: normalKebab, id: Math.random(), type: 'Kebab'},
		{name: 'Mixed', size: 'Normal', price: normalKebab, id: Math.random(), type: 'Kebab'}];
	
	let burgers = [
		{name: 'Chicken', size: 'Normal', price: normalBurger, id: Math.random(), type: 'Burger'},
		{name: 'Cheese', size: 'Normal', price: normalBurger, id: Math.random(), type: 'Burger'},
		{name: 'Double Cheese', size: 'Normal', price: normalBurger, id: Math.random(), type: 'Burger'},
		{name: 'Veggie', size: 'Normal', price: normalBurger, id: Math.random(), type: 'Burger'}];
	
	let sides = [
		{name: 'Chips', size: 'Normal', price: normalSide, id: Math.random(), type: 'Side'},
		{name: 'Onion Rings', size: 'Normal', price: normalSide, id: Math.random(), type: 'Side'},
		{name: 'Garlic Bread', size: 'Normal', price: normalSide, id: Math.random(), type: 'Side'},
		{name: 'Cheesy Garlic Bread', size: 'Normal', price: normalSide, id: Math.random(), type: 'Side'}];
	
	let deserts = [
		{name: 'Cheese Cake', size: 'Normal', price: normalDesert, id: Math.random(), type: 'Desert'},
		{name: 'Chocolate Cake', size: 'Normal', price: normalDesert, id: Math.random(), type: 'Desert'},
		{name: 'Strawberry cake', size: 'Normal', price: normalDesert, id: Math.random(), type: 'Desert'},
		{name: 'Ice Cream', size: 'Normal', price: normalDesert, id: Math.random(), type: 'Desert'},
		{name: 'Waffles', size: 'Normal', price: normalDesert, id: Math.random(), type: 'Desert'}];
	
	
	
	const setCat = (e) => {
		currentCategory = e.detail;
		
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
	};
	
	const addToCart = (e) => {
		const selectedItem = e.detail;
		selectedItems = [selectedItem, ...selectedItems];
		
		//Update Total
		updateTotal();
	};
	const removeFromCart = (e) => {
		const selectedItem = e.detail;
		const updatedSelectedItems = [...selectedItems];
		const updatedSelectedItem = updatedSelectedItems.find((item) => item.id == selectedItem.id);
		
		for(var i = 0; i < updatedSelectedItems.length; i++){
			if(updatedSelectedItems[i].id == updatedSelectedItem.id){
				updatedSelectedItems.splice(i, 1);
			}
		}
		selectedItems = updatedSelectedItems;
		//Update Total
		updateTotal();
	};
	
	const increaseQTY = (e) => {
		const selectedItem = e.detail;
		const updatedSelectedItems = [...selectedItems];
		const updatedSelectedItem = updatedSelectedItems.find((item) => item.id == selectedItem.id);
		
		//Update Sub-Total
		updatedSelectedItem.qty++;
		const subTotal = updatedSelectedItem.price * updatedSelectedItem.qty;
		updatedSelectedItem.sub = subTotal+".00";
		
		selectedItems = updatedSelectedItems;
		
		//Update Total
		updateTotal();
	};
	
	const decreaseQTY = (e) => {
		const selectedItem = e.detail;
		const updatedSelectedItems = [...selectedItems];
		const updatedSelectedItem = updatedSelectedItems.find((item) => item.id == selectedItem.id);
		
		//Update Sub-Total
		updatedSelectedItem.qty--;
		const subTotal = updatedSelectedItem.price * updatedSelectedItem.qty;
		updatedSelectedItem.sub = subTotal+".00";
		
		selectedItems = updatedSelectedItems;
		
		//Update Total
		updateTotal();
	};
	
	const checkOut = (e) => {
				
		//Checkout Alert
		alert('Thanks for checking out my simple shopping cart made with Svelte - By Nick Wright');
	};
	
	function updateTotal(){
		var newTotal = 0;
		for(var i = 0; i < selectedItems.length; i++){
			newTotal +=  parseFloat(selectedItems[i].price) * selectedItems[i].qty;
		}
		total = newTotal.toFixed(2);
		console.log(total);
	}
	
	const updateSize = (e) => {
		const {size, product} = e.detail;
		
		const updatedProducts = [...products];
		const updatedSelectedProduct = updatedProducts.find((item) => item.id == product.id);
		
		updatedSelectedProduct.size = size;
		if(size == 'Small'){			
			if(product.type == 'Drink'){
				updatedSelectedProduct.price = smallDrink;
			}
			if(product.type == 'Pizza'){
				updatedSelectedProduct.price = smallPizza;
			}
			if(product.type == 'Kebab'){
				updatedSelectedProduct.price = smallKebab;
			}
			if(product.type == 'Burger'){
				updatedSelectedProduct.price = smallBurger;
			}
			if(product.type == 'Side'){
				updatedSelectedProduct.price = smallSide;
			}
			if(product.type == 'Desert'){
				updatedSelectedProduct.price = smallDesert;
			}
		}
		if(size === 'Normal'){
			if(product.type == 'Drink'){
				updatedSelectedProduct.price = normalDrink;
			}
			if(product.type == 'Pizza'){
				updatedSelectedProduct.price = normalPizza;
			}
			if(product.type == 'Kebab'){
				updatedSelectedProduct.price = normalKebab;
			}
			if(product.type == 'Burger'){
				updatedSelectedProduct.price = normalBurger;
			}
			if(product.type == 'Side'){
				updatedSelectedProduct.price = normalSide;
			}
			if(product.type == 'Desert'){
				updatedSelectedProduct.price = normalDesert;
			}
		}
		if(size === 'Large'){
			if(product.type == 'Drink'){
				updatedSelectedProduct.price = largeDrink;
			}
			if(product.type == 'Pizza'){
				updatedSelectedProduct.price = largePizza;
			}
			if(product.type == 'Kebab'){
				updatedSelectedProduct.price = largeKebab;
			}
			if(product.type == 'Burger'){
				updatedSelectedProduct.price = largeBurger;
			}
			if(product.type == 'Side'){
				updatedSelectedProduct.price = largeSide;
			}
			if(product.type == 'Desert'){
				updatedSelectedProduct.price = largeDesert;
			}
		}
		
		products = updatedProducts;
	}
</script>

<style>
	.Centre{
		display: flex;
		position: relative;
		width: 100%;
	}
</style>

<Header/>
<main>
<div class="Centre">
<Categories {menuItem} on:setCat={setCat}/>
<Products {currentCategory} {products} {drinks} {pizzas} {kebabs} {burgers} {sides} {deserts} on:addToCart={addToCart}  on:updateSize={updateSize}/>
<Cart {selectedItems} {total} on:increaseQTY={increaseQTY} on:decreaseQTY={decreaseQTY} on:removeFromCart={removeFromCart} on:checkOut={checkOut}/>
</div>
</main>
<Footer/>