<template>
  <div class="hello">
    <create-todo v-on:todo-updated="addTodo" />
    <div class="todo-list">
      <div class="todo-list-wrap">
        <Todo
          v-for="(item, index) in openTodos"
          :key="index"
          v-on:todo-deleted="fetchData"
          :id="item.id"
          :title="item.title"
          :date="item.date"
          :beschreibung="item.desc"
          :status="item.isComplete"
          :important="item.important"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Todo from "@/components/Todo.vue";
import CreateTodo from "@/components/CreateTodo.vue";

export default {
  name: "ContentView",
  components: {
    Todo,
    CreateTodo,
  },
  props: ["showOpenTodos"],

  data() {
    return {
      todos: [],
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      axios({
        method: "get",
        url: "https://vue-todo-backend.azurewebsites.net/todos",
      })
        .then((result) => {
          this.todos = result.data;
        })
        .catch((e) => console.log("error", e))
        .finally(function () {
          console.log("Ich bin fertig");
        });
    },
    addTodo(todo) {
      this.todos.push(todo);
    },
  },
  computed: {
    openTodos() {
      return this.todos.filter(
        (todo) => todo.isComplete !== this.showOpenTodos
      );
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todo-list {
  display: block;
  width: 100vw;
  margin: 0 auto 80px;
  padding: 0;
}

button {
}

.todo-list-wrap {
  display: flex;
  margin: 0 auto;
  padding: 0;
  width: 95%;
  flex-direction: column;
  align-items: center;
}
</style>
