<template>
  <div>
    <h2>Todo Application</h2>
    <router-link to="/">Home</router-link>
    <hr>

    <AddTodo
      @add-todo='AddTodo'
    />
    <hr>
    <Loader v-if="loading" />
    <TodoList
    v-else-if="todos.length"
    v-bind:todos='todos'
    @remove-todo='removeTodo'
     />
    <p v-else>Список пуст</p>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList"
import AddTodo from "@/components/AddTodo"
import Loader from "@/components/Loader"
export default {
  name: 'App',
  data() {
    return{
      todos: [],
      loading: true
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=10')
  .then(response => response.json())
  .then(json => {
      setTimeout(() => {
    this.todos = json
    this.loading = false 
      }, 1000);

  })
  },
  methods: {
    removeTodo(id){
        this.todos = this.todos.filter(t => t.id !== id)
    },
    AddTodo(todo){
      this.todos.push(todo)
    }
  },
  components: {
    TodoList,
    AddTodo,
    Loader, 

  }
}
</script>