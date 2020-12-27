<template>
  <div id="app">
    <Header/>
    <Addtodo v-on:add-todo="addTodo" v-on:clear-all="clearall"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Header from './components/layout/Header';
import Todos from './components/Todos';
import Addtodo from './components/Addtodo';
import Vue from 'vue';
import lodash from 'lodash';
import VueLodash from 'vue-lodash';
Vue.use(VueLodash,{name:"custom",lodash:lodash})
const STORAGE_KEY="storagetodo"
export default {
  name: 'app',
  components: {
    Header,
    Addtodo,
    Todos
  },
  data(){
    return{
      todos:[]
    }
  },
  methods:{
    deleteTodo(id){
      this.todos = this.todos.filter(todo => todo.id !== id);
      localStorage.setItem(STORAGE_KEY,JSON.stringify(this.todos))
    },
    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo]
      localStorage.setItem(STORAGE_KEY,JSON.stringify(this.todos))
    },
    clearall(){
      this.todos=[]
      localStorage.setItem(STORAGE_KEY,JSON.stringify(this.todos))
    }
  },
  created(){
    this.todos=JSON.parse(localStorage.getItem(STORAGE_KEY) || "[]")
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

}
</style>
