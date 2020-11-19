<template>
  <div id="app">
    <div class="container grid-xs py-2">
      <img class="img-responsive img-logo" src="@/assets/todo.png" alt="Logo Todo">
      <form @submit.prevent="addTodo(todo)">
        <div class="input-group">
          <input 
          type="text" 
          class="form-input"
          v-model="todo.description" 
          placeholder="Novo Todo">
          <button class="btn btn-primary input-group-btn">Novo Todo</button>
        </div>
      </form>
        <div class="todo-list">
          <Todo v-for="t in todos" :key="t.id" @toggle="toggleTodo" @remove="removeTodo" :todo="t"/>
        </div>
    </div>
  </div>
</template>

<script>
import Todo from './components/Todo';
export default {
  name: 'App',
  components: { Todo },
  data() {
    return { todos: [], todo: { checked: false } }
  },
  methods: {
    addTodo(todo) {
     todo.id = Date.now();
     this.todos.push(todo);
     this.todo = { checked: false }
    },
    toggleTodo(todo) {
      const index = this.todos.findIndex(i => i.id === todo.id)
      if(index > -1) {
        const checked = !this.todos[index].checked;
        this.$set(this.todos, index, {...this.todos[index], checked})
      }
    },
    removeTodo(todo) {
      const index = this.todos.findIndex(i => i.id === todo.id)
      if(index > -1) {
        this.$delete(this.todos, index);
      }
    }
  }
}
</script>

<style scoped>
  .img-logo {
    display: flex;
    justify-content: center;
    max-width: 500px;
    margin: 0 auto;
    margin-bottom: 2rem;
  }
</style>
