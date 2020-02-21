<template>
  <div id="app">
   
  <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
   <AddTodo v-on:add-todo="addnewtodo" />

  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Todos from './components/Todos.vue'
import AddTodo from './components/AddTodo.vue'
import axios from 'axios';


export default {
  name: 'App',
  components: {
    Todos,AddTodo
  },
  methods:{
deleteTodo(id){
   axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
  .then(() => {this.todos = this.todos.filter(todo => todo.id !== id)})
  .catch(err => console.log(err));
    
},
addnewtodo(newTodo){
  const {title,completed} = newTodo;

  axios.post('https://jsonplaceholder.typicode.com/todos',{
    title,completed
  })
  .then(res => this.todos = [...this.todos,res.data])
  .catch(err => console.log(err));

  //[...this.todos,res.data] allow to add item res.data to array this.todos

}
  },
  created(){
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(res=> this.todos=res.data)
    .catch(err => console.log(err))
  },
  data(){
    return {
      todos: []
  }
}
}
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
*{
  box-sizing: border-box;
  margin:0px;
  padding:0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.5;
}
</style>
