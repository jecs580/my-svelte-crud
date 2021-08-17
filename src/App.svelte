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
	const delTodo = (id)=>{
		todoList = todoList.filter(item => item.id !==id);
	}
	const editTodo = (id)=>{
		todoList = todoList.map(item=> {
			return item.id ===id ? {...item, estado: !item.estado} : item
	})
	}
	const classIcono = valor =>(
		valor ? "bi bi-arrow-clockwise": "bi bi-check2"
	)
	const classEstado =valor =>valor?'btn-success':'btn-warning'
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
		<p
		class={item.estado?'text-decoration-line-through':''}
		>
			{item.content}
		</p>
		<button class="btn btn-sm {classEstado(item.estado)}" on:click={editTodo(item.id)}>
			<i class={classIcono(item.estado)}></i>
		</button>
		<button class="btn btn-sm btn-danger" on:click={delTodo(item.id)}>
			<i class="bi bi-trash"></i>
		</button>
	</div>
	{/each}
</div>