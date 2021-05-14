<template>
  <div>
    <h2>To Do List Application</h2>
    <router-link to='/'>Home</router-link>
    <br> <br>
    <AddToDo 
          @new-todo="CreateNewTodo"
          />
    <br>
    <div class="btns">
      <button @click="gatherLocalToDos">Use Local ToDoList</button>
      <button @click="gatherServerToDos">Use Server ToDoList</button>
    </div>
    <br>
    <select v-model='filter'>
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not Completed</option>
    </select>
    <br> <br>
    <hr>
    <br>
    <Loader v-if="loading"/>
    <ToDoList
      v-bind:todos="filteredToDos"
      v-on:removeTodo="removeTodo"
      v-else-if="filteredToDos.length"
    />
    <p v-else>No ToDos!</p>
    <br>

  </div>
</template>

<script>

import ToDoList from '@/components/ToDoList'
import AddToDo from '@/components/AddToDo'
import Loader from '@/components/Loader'

export default {
  name: 'App',

  data() {
    return {
      LocalTodos: [
      {id: 1, title: "JS", completed: false},
      {id: 2, title: "Vue", completed: false},
      {id: 3, title: "Wake up", completed: true}
    ],
      todos: [

      ],
      loading: true,
      filter: 'all'
    }
  },

  mounted() {
    this.todos = this.LocalTodos;
    this.loading = false;
  },

  // watch: {
  //   filter(value) {

  //   }
  // },

  computed: {
    filteredToDos() {
        if (this.filter === 'all') 
          return this.todos;
        else if (this.filter === 'completed')
          return this.todos.filter(element => element.completed)
        else if (this.filter === 'not-completed')
          return this.todos.filter(element => !element.completed)
    }
  },

  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },

    CreateNewTodo(newTodo) {
      this.todos.push(newTodo)
    },

    gatherServerToDos() {
          this.loading = true;
          this.todos = []
          fetch('https://jsonplaceholder.typicode.com/todos?_list=3')
          .then(response => response.json())
          .then(json => {
            setTimeout(() => {
              this.todos = json;
              this.loading = false;
            }, 1000)
         })
      },

      gatherLocalToDos() {
        this.todos = this.LocalTodos;
      }
  },

  components: {
    ToDoList,
    AddToDo,
    Loader
  },
  
}
</script>
