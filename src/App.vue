<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <h1>Todos</h1>
    <input type="text" v-model="todoName" @keyup.enter="addTodo" />
    <ul>
      <li v-for="todo of todos" :key="todo.id">{{ todo.name }}</li>
    </ul>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import axios from "axios";

const baseURL = "http://localhost:3000/todos";
export default {
  name: "App",
  components: {
    // HelloWorld
  },
  data() {
    return {
      todos: [
        // {
        // id: 1,
        // name: "helle todos",
        // },
      ],
      todoName: "",
    };
  },
  async created() {
    try {
      const res = await axios.get(baseURL);
      this.todos = res.data;
    } catch (e) {
      console.error(e);
    }
  },
  methods: {
    async addTodo() {
      const res = await axios.post(baseURL, { name: this.todoName });
      this.todos = [...this.todos, res.data];
      this.todoName = "";
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