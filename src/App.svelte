<script>
	import { Toast } from 'bootstrap'
	let toastEl;
	$:console.log(toastEl);
	let opc = {texto:'', color:''}
	const mostrarToast = (texto, color)=>{
		opc ={texto,color}
		new Toast(toastEl).show()
	}
	let todoList = []
	let todo ={
		id:'',
		content:'',
		state:false
	}
	if(localStorage.getItem('todoList')){
		todoList = JSON.parse(localStorage.getItem('todoList'));
	}
	$: localStorage.setItem('todoList',JSON.stringify(todoList))
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
		mostrarToast('Todo Agregado','bg-primary')
	}
	const delTodo = (id)=>{
		todoList = todoList.filter(item => item.id !==id);
		mostrarToast('Todo eliminado','bg-danger')
	}
	const editTodo = (id)=>{
		todoList = todoList.map(item=> {
			return item.id ===id ? {...item, estado: !item.estado} : item
		})
		mostrarToast('Todo Agregado','bg-warning')
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
	<div class="toast-container position-absolute p-3 top-0 end-0">
		<div bind:this={toastEl} class="toast align-items-center text-white {opc.color} border-0" role="alert" aria-live="assertive" aria-atomic="true">
			<div class="d-flex">
			  <div class="toast-body">
				{opc.texto}
			  </div>
			  <button type="button" class="btn-close btn-close-white me-2 m-auto" data-bs-dismiss="toast" aria-label="Close"></button>
			</div>
		</div>
	</div>
</div>