<template>
  <div id="app">
    <input type="text" @keydown="addTodo" v-model="todo" />
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
export default {
  name: "app",
  components: {},
  data: function () {
    return {
      todo: "",
      newTodo: "",
      todoList: [
        {
          id: 1,
          todo: "talk with friends",
          isCompleted: false,
          isEdited: false,
        },
        {
          id: 2,
          todo: "go to gym",
          isCompleted: false,
          isEdited: false,
        },
        {
          id: 3,
          todo: "drink water",
          isCompleted: false,
          isEdited: false,
        },
        {
          id: 4,
          todo: "studt vue",
          isCompleted: false,
          isEdited: false,
        },
      ],
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
    addTodo: function (e) {
      if (e.keyCode !== 13) return;
      let length = this.todoList.length;
      const newObj = {
        // id 중복 에러!!
        // id: this.todoList.length + 1,
        // 무조건 마지막 todo의 id 값에 + 1을 해준다
        // 즉, 새로 생성하는 id가 배열의 length 를 기준으로 만들어지는지, 마지막 id를 기준으로 만들어지는지가 다르다.
        id: this.todoList[length - 1].id + 1,
        todo: this.todo,
        isCompleted: false,
      };
      this.todoList.push(newObj);
      console.log("this.todoList: ", this.todoList);
      console.log("length: ", length);
      console.log("id + 1: ", this.todoList[length - 1].id + 1);
      this.todo = "";
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
  },
};

// issue
// todo가 생성될 때 `id`가 중복되어 에러
</script>

<style></style>
