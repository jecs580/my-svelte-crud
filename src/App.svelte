<script>
	let todoList = []
	let todo ={
		id:'',
		content:'',
		state:false
	}
	const addTodo = ()=>{
		if(!todo.content.trim()){
			console.log('Texto vacio');
			todo.content =''
			return
		}
		todo.id = Date.now()
		todoList = [... todoList, todo]
		console.log(todoList);
		todo = {
			id:'',
			content:'',
			state:false
		}
	}
</script>
<div class="container">
	<h1 class="display-5 my-3"> CRUD</h1>
	<form on:submit|preventDefault={addTodo}>
		<input
			type="text"
			placeholder="Enter para agregar una tarea"
			class="form-control shadow border-0"
			bind:value={todo.content}
		>
	</form>
	{#each todoList as item}
	<div class="shadow my-3 p-3 lead">
		<p>
			{item.content}
		</p>
		<button class="btn btn-sm btn-warning">
			<i class="bi bi-check2"></i>
		</button>
		<button class="btn btn-sm btn-danger">
			<i class="bi bi-trash"></i>
		</button>
	</div>
	{/each}
</div>