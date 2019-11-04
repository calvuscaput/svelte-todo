<script>
  import TodoItem from './TodoItem.svelte'

  let newTodoTitle = '';
  let currentFilter = 'all';
  let nextId = 4;

  let todos = [
    {
      id: 1,
      title: 'My first todo',
      completed: false
    },
    {
      id: 2,
      title: 'My second todo',
      completed: false
    },
    {
      id: 3,
      title: 'My third todo',
      completed: false
    }
  ];
</script>

<div class="container">
  <img src={'http://place-puppy.com/200x200'} alt="Todo list">
  <h2>Svelte Todo App</h2>
  <input 
    type="text"
    class="todo-input" 
    placeholder="Insert Todo item"
    bind:value={newTodoTitle} 
    on:keydown={addTodo}
  />

  {#each filteredTodo as todo}
    <div class="todo-item">
      <TodoItem
        {...todo}
        on:deleteTodo={handleDeleteTodo}
        on:toggleComplete={handleToggleComplete}

      />
    </div>
  {/each}

  <div class="inner-container">
    <div>
      <label>
        <input
          type="checkbox" 
          class="inner-container-input"
          on:change={checkAllTodos}
        >
        Check All
      </label>
    </div>
    <div>{todosRemaining} items left</div>
  </div>

  <div class="inner-container">
    <div>
      <button
        on:click={() => updateFilter('all')}
        class:active="{currentFilter === 'all'}"
      >
      All
      </button>
      <button
        on:click={() => updateFilter('active')}
        class:active="{currentFilter === 'active'}"
      >
      Active
      </button>
      <button
        on:click={() => updateFilter('completed')}
        class:active="{currentFilter === 'completed'}"
      >
      Completed
      </button>
    </div>
    <div>
      <button on:click={clearCompleted}>Clear Completed</button>
    </div>
  </div>
</div>