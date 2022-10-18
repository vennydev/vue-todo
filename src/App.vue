<template>
  <div id="app">
    <todo-input v-on:submit="addTodo"></todo-input>
    <todo-list></todo-list>
    <todo-footer></todo-footer>
    <table>
      <thead>
        <tr>
          <th>No</th>
          <th>Todo</th>
          <th>Done</th>
          <th>Edit</th>
          <th>Delete</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="(todo, index) in todoList" :key="'todo_' + todo.id">
          <td>{{ todo.id }}</td>
          <td v-if="!todo.isEdited">{{ todo.todo }}</td>
          <td v-else>
            <input
              type="text"
              :placeholder="todo.todo"
              @keydown="editTodo($event, index)"
              v-model="newTodo"
            />
          </td>
          <td>
            <button @click="handleDone(index)">{{ todo.isCompleted }}</button>
          </td>
          <td>
            <button @click="handleEdit(index)">Edit</button>
          </td>
          <td>
            <button @click="deleteTodo(index)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";

export default {
  name: "app",
  components: {
    TodoInput,
    TodoList,
    TodoFooter,
  },
  data: function () {
    return {
      newTodo: "",
      todoList: [],
    };
  },
  methods: {
    handleDone: function (index) {
      if (this.todoList[index].isCompleted === false) {
        this.todoList[index].isCompleted = true;
      } else {
        this.todoList[index].isCompleted = false;
      }
    },
    deleteTodo: function (index) {
      // let fileteredList = this.todoList.filter((item) => item.id !== id);
      // this.todoList = fileteredList;
      this.todoList.splice(index, 1);
    },
    handleEdit: function (index) {
      this.todoList[index].isEdited = !this.todoList[index].isEdited;
    },
    editTodo: function (e, index) {
      if (e.keyCode !== 13) return;
      // console.dir(e.target.value, index);
      this.todoList[index].todo = this.newTodo;
      this.handleEdit(index);
      this.newTodo = "";
    },
    addTodo: function (todo) {
      console.log("todo: ", todo);
      let newObj = {
        id: this.todoList.length + 1,
        todo: todo,
        isCompleted: false,
      };
      this.todoList.push(newObj);
    },
  },
};

// issue
// todo가 생성될 때 `id`가 중복되어 에러
</script>

<style></style>
