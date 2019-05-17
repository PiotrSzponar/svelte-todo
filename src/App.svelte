<script>

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
      font-size: 24px;
      color: #2c3e50;
      margin-left: 12px;
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc; //override defaults
      font-family: "Avenir", Helvetica, Arial, sans-serif;
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
  <img src={'/img/svelte-logo-horizontal.svg'} alt="svelte logo" class="logo" />

  <input type="text" class="todo-input" placeholder="What needs to be done" />

  <div class="todo-item">
    <div class="todo-item-left">
      <input type="checkbox" />
      <div class="todo-item-label">title</div>
    </div>
    <div class="remove-item">×</div>
  </div>

  <div class="extra-container">
    <div>
      <label>
        <input type="checkbox" />
        Check All
      </label>
    </div>
    <div>10 items left</div>
  </div>

  <div class="extra-container">
    <div>
      <button>All</button>
      <button>Active</button>
      <button>Completed</button>
    </div>

    <div>
      <button>Clear Completed</button>
    </div>
  </div>
</div>
