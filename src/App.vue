<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <div id="todo-wrapper">
    <input type="text" v-model="newTodo" />
    <button @click="addTodo">Submit</button>

    <div v-for="(singleTodo, index) in filteredTodo" v-bind:key="index">
      <input
        v-if="singleTodo.editing"
        v-model="singleTodo.content"
        v-on:keyup.enter="singleTodo.editing = false"
      />
      <Todo
        v-else
        v-bind:todo="singleTodo"
        v-on:editTodo="todoEdit(index)"
        v-on:completeTodo="todoCompleted(index)"
        v-on:unmarkTodo="todoUnmarked(index)"
      />
    </div>

    <select name="Filter" id="" v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="active">Active</option>
    </select>
  </div>
</template>

<script>
import Todo from "./components/Todo.vue";
export default {
  name: "App",
  components: {
    Todo,
  },
  data() {
    return {
      todos: [
        {
          content: "Todo 1",
          is_completed: false,
          editing: true,
        },
        {
          content: "Todo 2",
          is_completed: true,
          editing: false,
        },
        {
          content: "Todo 3",
          is_completed: false,
          editing: false,
        },
      ],
      newTodo: "",
      filter: "all",
    };
  },
  computed: {
    filteredTodo() {
      if (this.filter === "active") {
        return this.todos.filter((todo) => todo.is_completed === false);
      } else if (this.filter === "completed") {
        return this.todos.filter((todo) => todo.is_completed === true);
      }
      return this.todos;
    },
  },
  methods: {
    addTodo() {
      if (!this.newTodo) return;
      this.todos.push({
        content: this.newTodo,
        is_completed: false,
      });
      this.newTodo = "";
    },
    todoCompleted(index) {
      this.todos[index].is_completed = true;
    },
    todoUnmarked(index) {
      this.todos[index].is_completed = false;
    },
    todoEdit(index) {
      this.todos[index].editing = true;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
