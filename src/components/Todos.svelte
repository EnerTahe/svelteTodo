<script>
    import '../styles.css'

    let todoItems = [];
    let newTodo = '';
  
    function addTodo() {
      newTodo = newTodo.trim();
      if (!newTodo) return;
  
      const todo = {
        text: newTodo,
        checked: false,
        id: Date.now(),
      };
  
      todoItems = [...todoItems, todo];
      newTodo = '';
    }
  
    function toggleDone(id) {
      const index = todoItems.findIndex((item) => item.id === Number(id));
      todoItems[index].checked = !todoItems[index].checked;
    }
  
    function deleteTodo(id) {
      todoItems = todoItems.filter((item) => item.id !== Number(id));
    }
</script>
  
  <div class="todo-list-container">
    <h1 class="todo-list-title">My to-do list</h1>
  
    <form class="todo-form" on:submit|preventDefault={addTodo}>
      <input
        class="todo-input"
        type="text"
        aria-label="Enter a new todo item"
        placeholder="Enter a new todo item"
        bind:value={newTodo}
      />
    </form>
  
    <ul class="todo-list">
        {#each todoItems as todo (todo.id)}
          <li class="todo-item {todo.checked ? 'done' : ''}">
            <label class="checkbox-container">
              <input
                class="checkbox-input"
                id={todo.id}
                type="checkbox"
                checked={todo.checked}
                on:change={() => toggleDone(todo.id)}
              />
              <span class="checkbox-custom"></span>
            </label>
            <span>{todo.text}</span>
        <button class="delete-todo" on:click={() => deleteTodo(todo.id)}>
          <svg xmlns="http://www.w3.org/2000/svg" height="20px" viewBox="0 0 448 512">
            <path d="M135.2 17.7L128 32H32C14.3 32 0 46.3 0 64S14.3 96 32 96H416c17.7 0 32-14.3 32-32s-14.3-32-32-32H320l-7.2-14.3C307.4 6.8 296.3 0 284.2 0H163.8c-12.1 0-23.2 6.8-28.6 17.7zM416 128H32L53.2 467c1.6 25.3 22.6 45 47.9 45H346.9c25.3 0 46.3-19.7 47.9-45L416 128z" />
          </svg>
        </button>
      </li>
      {/each}
    </ul>
  </div>
  
  