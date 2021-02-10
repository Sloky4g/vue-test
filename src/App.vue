<template>
  <div class="container">
    <form class="add-form">
      <span class="p-float-label">
        <InputText id="todo" type="text" v-model="text" />
        <label for="todo">Add a new todo</label>
      </span>
      <Button label="Add" icon="pi pi-pencil" @click="addTodo(text)" />
    </form>
    <ul v-if="todos.length">
      <li class="todo-item" v-for="(todo, index) in todos" :key="index" >
        <span>{{ todo.name }}</span><Button icon="pi pi-trash" @click="deleteTodo(index)" />
      </li>
    </ul>
    <span v-else>No todos</span>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'App',
  data() {
    return {
      text: '',
      todos: [
        {id: 1, name: 'todo1'},
        {id: 2, name: 'todo2'}
      ]
    }
  },
  methods: {
    addTodo(text: string) {
      if (text.trim()) {
        const newTodo = {
          id: Date.now(),
          name: text
        }

        this.todos.push(newTodo)
        this.text = ''
      }
    },
    deleteTodo(i: number) {
      this.todos.splice(i, 1)
    }
  }
});
</script>

<style scoped>
  .container {
    width: 600px;
    margin: 60px auto 0;
  }
  .p-float-label {
    width: 100%;
  }
  .p-float-label input {
    width: 100%;
  }
  .add-form {
    display: flex;
    justify-content: center;
    margin-bottom: 20px;
  }
  ul {
    list-style: none;
    font-size: 1.5rem;
    padding: 0;
  }
  .todo-item {
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
  }
</style>
