<script context="module">
  const fn = "TodoForm.svelte";
</script>

<script>
  // function from parent
  export let addTodo;
  let newTodo = resetTodo();

  function resetTodo() {
    return {
      title: "",
      done: false,
      dueDate: "",
    };
  }
  function formSubmitted() {
    console.log(`${fn}: ${JSON.stringify(newTodo)}`);
    addTodo(newTodo);
    newTodo = resetTodo();
  }
</script>

<form on:submit|preventDefault={formSubmitted}>
  <label for="txtTitle">
    New Todo
    <input bind:value={newTodo.title} name="title" id="txtTitle" type="text" placeholder="Enter a todo..." />
  </label>
  <label for="txtDueDate">
    Due Date
    <input type="date" name="dueDate" id="txtDueDate" bind:value={newTodo.dueDate} />
  </label>
  <h4>{JSON.stringify(newTodo)}</h4>
  <button>Add Todo</button>
</form>

<style>
</style>
