<template>
  <div id="app">
    <h1>Todos</h1>
    <input type="text" v-model="todoName" @keyup.enter="addTodo">
    <ul>
      <li v-for="todo of todos" :key="todo.id">
        {{ todo.title}}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";

const baseURL = "https://jsonplaceholder.typicode.com/todos?_limit=5"

export default {
  name: 'app',
  data(){
    return{
      todos: [],
      todoname: ''
    }
  },
  components: {
  },
  created(){
    axios.get(baseURL)
    .then(res=> this.todos = res.data)
    .catch(err => console.log(err))
  },
  methods: {
    addTodo(newTodo){
      const title = newTodo;
        axios.post(baseURL, title)
        .then(res => this.todos = [...this.todos, newTodo])
        .catch(err => console.log(err))
    }
  }

}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
