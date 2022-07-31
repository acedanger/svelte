<script context="module">
  const fn = "App.svelte";
  import { format } from "date-fns";
</script>

<script>
  import TodoForm from "./lib/TodoForm.svelte";
  // array of todo objects
  let todos = localStorage.getItem("todos") ? JSON.parse(localStorage.getItem("todos")) : [];

  /**
   * Save todo item
   * @param {Object} todo - Todo object
   * @param {string} todo.title - Name of the todo item
   * @param {boolean} todo.done - Todo item done
   * @param {Date?} todo.dueDate - Date todo is due
   */
  function addTodo(todo) {
    if (todo.title === "") return;

    todos.push(todo);
    todos = todos; // force reactivity
    console.log(`${fn}: ${JSON.stringify(todos)}`);
  }

  /**
   * Delete todo item
   * @param {number} index - index of `todo` item in the `todos` array
   */
  function removeTodo(index) {
    todos.splice(index, 1);
    todos = todos; // force reactivity
  }

  // whenever the `todos` array has changed, write it to local storage
  $: localStorage.setItem("todos", JSON.stringify(todos));
</script>

<main>
  <h3>Today is {format(new Date(), "M-d-yyyy")}</h3>
  <div>
    <!-- {addTodo} is the local function passed to the TodoForm component -->
    <TodoForm {addTodo} />
  </div>
  <div>
    <ul>
      {#each todos as todo, index}
        <li class="todo">
          {#if todo.done}
            <span>✅</span>
          {/if}
          <span on:click={() => (todo.done = !todo.done)} class:done={todo.done}>
            {todo.title}
          </span>
          <span class="delete" on:click={() => removeTodo(index)}>🗑️</span>
        </li>
      {/each}
    </ul>
  </div>
</main>

<style>
  .todo {
    cursor: pointer;
  }
  .done {
    text-decoration: line-through;
  }
  .delete {
    display: inline-block;
  }
  .delete:hover {
    transform: scale(2);
  }
</style>
