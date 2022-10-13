<template>
  <div id="app">
    <header class="">
      <h1>todos</h1>
    </header>
    <section class="todo-main">
      <input type="text" />
      <ul class="todo-list">
        <li class="todo">study</li>
        <li class="todo">work</li>
        <li class="todo">exercise</li>
      </ul>
      <footer>
        <p>2 items left</p>
        <ul class="sort-button">
          <li><button>All</button></li>
          <li><button>Active</button></li>
          <li><button>Completed</button></li>
        </ul>
      </footer>
    </section>
    <footer>
      <p>
        Made by <a href="https://github.com/vennydev/vue-todo">Venny Lee</a>
      </p>
    </footer>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
};
</script>

<style></style>
