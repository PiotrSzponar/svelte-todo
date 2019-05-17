<script>
  import { fade } from "svelte/transition";

  const ENTER_KEY = 13;

  let currentFilter = "all";
  let newTodo = "";

  let todos = [
    {
      id: 1,
      completed: false,
      title: "Go to store",
      editing: false
    },
    {
      id: 2,
      completed: false,
      title: "Finish Svelte tutorial",
      editing: false
    },
    {
      id: 3,
      completed: false,
      title: "Take over world",
      editing: false
    }
  ];

  const addTodo = e => {
    if (e.which === ENTER_KEY) {
      todos = [
        ...todos,
        {
          id: todos.length + 1,
          completed: false,
          title: newTodo,
          editing: false
        }
      ];
      newTodo = "";
    }
  };

  const deleteTodo = id => {
    todos = todos.filter(todo => todo.id !== id);
  };

  const checkAllTodos = e => {
    todos.forEach(todo => (todo.completed = e.target.checked));
    todos = todos;
  };

  const clearCompleted = () => {
    todos = todos.filter(todo => !todo.completed);
  };

  const updateFilter = filter => {
    currentFilter = filter;
  };

  const editTodo = todo => {
    todo.editing = true;
    todos = todos;
  };

  const doneEdit = todo => {
    todo.editing = false;
    todos = todos;
  };

  const doneEditEnter = (todo, e) => {
    if (e.which === ENTER_KEY) {
      doneEdit(todo);
    }
  };

  $: todosRemaining = todos.filter(todo => !todo.completed).length;

  $: filteredTodos =
    currentFilter === "all"
      ? todos
      : currentFilter === "completed"
      ? todos.filter(todo => todo.completed)
      : todos.filter(todo => !todo.completed);
</script>

<style lang="scss">
  .container {
    max-width: 600px;
    margin: 0 auto;
  }

  .logo {
    display: block;
    margin: 20px auto;
    height: 75px;
  }

  .info {
    font-size: 16px;
    color: #aaa;
    text-align: center;
    margin: 10px auto 20px;
    padding: 0;
    list-style: none;
  }

  .todo-input {
    width: 100%;
    padding: 10px 18px;
    font-size: 18px;
    margin-bottom: 16px;
  }

  .todo-item {
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    animation-duration: 0.3s;

    &-left {
      display: flex;
      align-items: center;
    }

    &-label {
      padding: 10px;
      border: 1px solid white;
      margin-left: 12px;

      &::first-letter {
        text-transform: uppercase;
      }
    }

    &-edit {
      color: #2c3e50;
      margin-left: 45px;
      width: 100%;
      font-size: 20px;

      &:focus {
        outline: none;
      }
    }
  }

  .remove-item {
    cursor: pointer;
    margin-left: 14px;
    font-size: 30px;

    &:hover {
      color: black;
    }
  }

  .completed {
    text-decoration: line-through;
    color: grey;
  }

  .extra-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 16px;
    border-top: 1px solid lightgrey;
    padding-top: 14px;
    margin-bottom: 14px;

    input {
      margin-right: 8px;
    }
  }

  button {
    font-size: 14px;
    background-color: white;
    appearance: none;
    cursor: pointer;
    transition: background-color 0.3s;

    &:hover {
      background-color: salmon;
    }
    &:focus {
      outline: none;
    }
  }

  .active {
    background-color: salmon;
  }
</style>

<div class="container">
  <img
    src={'./img/svelte-logo-horizontal.svg'}
    alt="svelte logo"
    class="logo" />

  <ul class="info">
    <li>➧ Press Enter to add new item.</li>
    <li>➧ Click at item name to edit it.</li>
  </ul>

  <input
    type="text"
    class="todo-input"
    placeholder="What needs to be done"
    bind:value={newTodo}
    on:keydown={addTodo} />

  {#each filteredTodos as todo}
    <div class="todo-item">
      <div class="todo-item-left" transition:fade>
        {#if !todo.editing}
          <input type="checkbox" bind:checked={todo.completed} />
          <div
            class="todo-item-label"
            class:completed={todo.completed}
            on:click={() => editTodo(todo)}>
             {todo.title}
          </div>
        {:else}
          <input
            type="text"
            class="todo-item-edit"
            bind:value={todo.title}
            on:blur={() => doneEdit(todo)}
            on:keydown={e => doneEditEnter(todo, e)}
            autofocus />
        {/if}
      </div>
      <div class="remove-item" on:click={() => deleteTodo(todo.id)}>×</div>
    </div>
  {/each}

  <div class="extra-container">
    <div>
      <label>
        <input type="checkbox" on:change={checkAllTodos} />
        Check All
      </label>
    </div>
    <div>{todosRemaining} items left</div>
  </div>

  <div class="extra-container">
    <div>
      <button
        on:click={() => updateFilter('all')}
        class:active={currentFilter === 'all'}>
        All
      </button>
      <button
        on:click={() => updateFilter('active')}
        class:active={currentFilter === 'active'}>
        Active
      </button>
      <button
        on:click={() => updateFilter('completed')}
        class:active={currentFilter === 'completed'}>
        Completed
      </button>
    </div>

    <div>
      <button on:click={clearCompleted}>Clear Completed</button>
    </div>
  </div>
</div>
