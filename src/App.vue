<template>
  <div id="app">
    <h1 class="title white-color">David's Aplikasi Todo</h1>
    <div class="field has-addons">
      <div class="control is-expanded">
        <input 
        class="input is-dark" 
        v-model="description" 
        type="text" 
        placeholder="Masukkan Apa Saja....."
        />
      </div>
      <div class="control">
        <a class="button is-dark" @click="addTodo" :disabled="!description">Tambahkan</a>
      </div>
    </div>
    <div class="notification" v-for="(todo, i) in todos" :key="todo._id">
      <div class="columns">
          <input class="column input" v-if="isSelected(todo)" v-model="editedDescription" />
          <p v-else class="column white-color">
            <span class="tag is-light">{{ i + 1 }}</span>
            {{ todo.description }}
          </p>
          <div class="column is-narrow">
            <span class="icon has-text-light" @click="removeTodo(todo, i)">
              <i class="material-icons">{{'delete'}}</i>
            </span>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'App',
  data() {
    return {
      todos: [],
      description: "",
      editedDescription: "",
      selected: {}
    }
  },

  async mounted() {
    const response = await axios.get('http://localhost:3000/todo')
    this.todos = response.data
  },
  
  methods: {
    async addTodo() {
      const response = await axios.post('http://localhost:3000/todo', {
        description: this.description
      });
      this.todos.push(response.data)
      this.description = ""
      alert('Data berhasil ditambahkan')
    },
    async removeTodo(todo, i) {
      await axios.delete("http://localhost:3000/todo/" + todo._id)
      this.todos.splice(i, 1)
    },
    select(todo) {
      this.selected = todo
      this.editedDescription = todo.description
    },
    isSelected(todo) {
      return todo._id === this.selected._id;
    },
    unselect() {
      this.selected = {};
      this.editedDescription = "";
    },
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins&display=swap');
#app {
  margin: auto;
  margin-top: 3rem;
  max-width: 700px;
  padding: 20px;
  background-color: #2C3E50;
  border-radius: 10px;
  font-family: 'Poppins', Arial, Helvetica, sans-serif;
}

i {
  cursor: pointer;
}

.notification {
  background-color: #85929E;
}

.white-color {
  color: white;
}

</style>
