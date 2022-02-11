<template>
  <div class="app-container">
    <h1 class="app-title">Vuejs todos</h1>

    <div class="composer">
      <AddTodo
        @addTask="addTask"
        @typeing="typeingHendeler"
        v-model="taskName"
      />

      <FilterTodo
        :allTodosLength="allTodosLength"
        :allPendingTodos="allPendingTodos"
        :allDoneTodos="allDoneTodos"
        @clear="clearTodo"
        @allTodo="filter__mode = 'All'"
        @pendingTodo="filter__mode = 'Pending'"
        @doneTodo="filter__mode = 'Done'"
      />
    </div>

    <div class="todos">
      <Todo
        v-for="todo in filterMode"
        :key="todo.id"
        :todo="todo"
        @changStatus="changStatus"
      />
    </div>
  </div>
</template>

<script>
import { v4 as uid } from "uuid";
import AddTodo from "./components/AddTodo.vue";
import FilterTodo from "./components/FilterTodo.vue";
import Todo from "./components/Todo.vue";
export default {
  mounted() {
    this.todos = JSON.parse(localStorage.getItem("todos"));
  },
  updated() {
    localStorage.setItem("todos", JSON.stringify(this.todos));
  },

  data() {
    return {
      taskName: "",
      todos: [],
      filter__mode: "All",
    };
  },
  methods: {
    typeingHendeler(e) {
      this.taskName = e.target.value;
    },

    addTask(e) {
      e.preventDefault();
      if (this.taskName !== "") {
        this.todos.unshift({
          id: uid(),
          task: this.taskName,
          status: false,
          time: new Date(),
        });
        this.taskName = "";
      } else {
        alert("Please enter a task");
      }
    },

    changStatus(todo) {
      todo.status = !todo.status;
    },

    clearTodo() {
      this.todos = this.todos.filter((todo) => !todo.status);
    },
  },
  components: {
    Todo,
    AddTodo,
    FilterTodo,
  },
  computed: {
    allTodosLength() {
      return this.todos.length;
    },
    allPendingTodos() {
      return this.todos.filter((todo) => !todo.status).length;
    },
    allDoneTodos() {
      return this.todos.filter((todo) => todo.status).length;
    },

    filterMode() {
      if (this.filter__mode === "All") return this.todos;
      if (this.filter__mode === "Pending")
        return this.todos.filter((todo) => !todo.status);
      if (this.filter__mode === "Done")
        return this.todos.filter((todo) => todo.status);
    },
  },
};
</script>
