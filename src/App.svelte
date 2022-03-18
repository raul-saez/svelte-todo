<script lang="ts">
	type TODO = {
		text: string
		status: boolean
	}

	let newItem = '';
	let todoList: TODO[] = [
		{text: 'Create Svelte TODO', status: true},
		{text: 'Test 1', status: false},
		{text: 'Test 2', status: false},
	];
	
	function addTODO() {
		todoList = [...todoList, {text: newItem, status: false}];
		newItem = '';
	}
	
	function removeTODO(index: number) {
		todoList.splice(index, 1)
		todoList = todoList;
	}
</script>

<input bind:value={newItem} type="text" placeholder="Type todo item...">
<button on:click={addTODO}>Add</button>

<br/>

<h3>TODO:</h3>
{#each todoList as item, index}
	{#if !item.status}
		<input bind:checked={item.status} type="checkbox">
		<span class:checked={item.status}>{item.text}</span>
		<button on:click={() => removeTODO(index)}>Remove</button>
		<br/>
	{/if}
{/each}

<hr />

<h3>Complete:</h3>
{#each todoList as item, index}
	{#if item.status}
		<input bind:checked={item.status} type="checkbox">
		<span class:checked={item.status}>{item.text}</span>
		<button on:click={() => removeTODO(index)}>Remove</button>
		<br/>
	{/if}
{/each} 


<style> 
	.checked {
		opacity: .5;
		text-decoration: line-through;
	}
</style> 