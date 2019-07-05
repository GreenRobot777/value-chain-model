<script>
	let yes = false;
  let a = 1;

  function resolve_sum(values) {
	  if (values.sum === undefined) {
	    values.sum = values.addend_first + values.addend_second;
	  }
	  if (values.addend_first === undefined) {
	    values.addend_first = values.sum - values.addend_second;
	  }
	  if (values.addend_second === undefined) {
	    values.addend_second = values.sum - values.addend_first;
	  }
	  return values;
	}
	
	function resolve_multiplication(values) {
	  if (values.product === undefined) {
	    values.product = values.multiplier_first * values.multiplier_second;
	  }
	  if (values.multiplier_first === undefined) {
	    values.multiplier_first = values.product / values.multiplier_second;
	  }
	  if (values.multiplier_second === undefined) {
	    values.multiplier_second = values.product / values.multiplier_first;
	  }
	  return values;
	}
	
	function test() {
	  values = new Object();
	
	  values.addend_first = 10;
	  values.addend_second = 20;
	  values.sum = undefined;
	  result = resolve_sum(values);
	  console.log(result);
	  
	  values.addend_first = 10;
	  values.addend_second = undefined;
	  values.sum = 30;
	  result = resolve_sum(values);
	  console.log(result);
	
	  values.addend_first = undefined;
	  values.addend_second = 20;
	  values.sum = 30;
	  result = resolve_sum(values);
	  console.log(result);
	}
	
	// test();
	
	let indicators = {
		cls: 100,
		ltv: 5000,
		revenue: 0,
		total_cost: 100000,
		profit: 0,
	}
	
	// indicators.revenue = indicators.cls * indicators.ltv;

	let values = {
		multiplier_first: indicators.cls,
		multiplier_second: indicators.ltv,
	}
	indicators.revenue = resolve_multiplication(values).product;
	
	values = {
		addend_first: indicators.revenue,
		addend_second: -1 * indicators.total_cost,
	}
	indicators.profit = resolve_sum(values).sum;
	
	// function get_revenue(cls, ltv) {
	//   return cls * ltv;
	// }
	// var revenue = get_revenue(cls, ltv);
	
	// function get_profit(revenue, total_cost) {
	//   return revenue - total_cost;  
	// }
	// var profit = get_profit(revenue, total_cost);
	
	console.log(indicators.profit);
	
	// HTML
	var msg = 'Profit = ' + indicators.profit;
	var icon = ' <i class="fa fa-smile-o"></i>'
	
	// $('#msg').html(msg + icon);

	let todos = [
		{ done: false, text: 'finish Svelte tutorial' },
		{ done: false, text: 'build an app' },
		{ done: false, text: 'world domination' }
	];

	function add() {
		todos = todos.concat({ done: false, text: '' });
	}

	function clear() {
		todos = todos.filter(t => !t.done);
	}

	$: remaining = todos.filter(t => !t.done).length;
</script>

<style>
	.done {
		opacity: 0.4;
	}
</style>

<!--
<h1>Todos</h1>

{#each todos as todo}
	<div class:done={todo.done}>
		<input
			type=checkbox
			checked={todo.done}
		>

		<label>
		    <input type=number bind:value={a} min=0 max=1000 placeholder="{a}">
		    <input type=range bind:value={a} min=0 max=1000>
		</label>

		<input
			placeholder="What needs to be done?"
			value={todo.text}
		>
	</div>
{/each}

<p>{remaining} remaining</p>

<button on:click={add}>
	Add new
</button>

<button on:click={clear}>
	Clear completed
</button>-->

<label>
    <input type=number bind:value={a} min=0 max=1000>
    <input type=range bind:value={a} min=0 max=1000>
</label>

<label>
    <!--<input type=number bind:value={indicators.profit} min=0 max=1000000>-->
    <!--<input type=range bind:value={indicators.profit} min=0 max=1000000>-->
</label>

<p>{a} + {indicators.profit} = {a + indicators.profit}</p>
<!--
<label>
	<input type=checkbox bind:checked={yes}>
	Yes! Send me regular email spam
</label>

{#if yes}
	<p>Thank you. We will bombard your inbox and sell your personal details.</p>
{:else}
	<p>You must opt in to continue. If you're not paying, you're the product.</p>
{/if}

<button disabled={!yes}>
	Subscribe
</button>-->