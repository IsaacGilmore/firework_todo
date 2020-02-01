<template>
<div id="app">
  <div v-if="fireworks" class="pyro">
    <div class="before"></div>
    <div class="after"></div>
  </div>
  <h2 id="main-title">todos</h2>
  <el-row type="flex" justify="center">
    <el-col :span="18">
      <el-input class="input" placehold="What needs to be done?" v-model="newTodo" @keyup.enter.native="addTodo">
        <el-button slot="append" icon="el-icon-check" @click="addTodo"></el-button>
      </el-input>
    </el-col>
  </el-row>
  <app-todo v-for="(todo, index) in todos" :todoName="todo.name" :key="index" @todo-deleted="deleteTodo" @todo-completed="completeTodo">
  </app-todo>
</div>
</template>

<script>
import AppTodo from './components/Todo.vue';

export default {
  data() {
    return {
      newTodo: '',
      todoTotal: '',
      fireworks: false,
      todos: [{
          name: 'Emails',
          completed: false,
          id: 1
        },
        {
          name: 'Other Stuff',
          completed: false,
          id: 2
        }
      ]
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo) {
        this.todos.unshift({
          name: this.newTodo,
          completed: false,
          id: this.todos.length + 1
        });
        this.newTodo = '';
      }
    },
    deleteTodo(todoName) {
      window.console.log(todoName);
      for (let i = 0; i < this.todos.length; i++) {
        if (todoName === this.todos[i].name) {
          this.todos.splice(i, 1);
        }
      }
    },
    openMessage(todoName) {
      this.$alert('You completed ' + todoName, 'Yay!', {
         confirmButtonText: 'OK'
      }).then(()=>{this.fireworks = false});
    },
    completeTodo(todoName) {
      for (let i = 0; i < this.todos.length; i++) {
        if (todoName === this.todos[i].name) {
          this.todos.splice(i, 1);
        }
        this.openMessage(todoName);
        this.fireworks = true;
      }
    }
  },
  components: {
    'app-todo': AppTodo
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Anonymous+Pro&display=swap');
@import './plugins/fireworks.css';
body {
  font-family: 'Anonymouse Pro', monospace;
}

#main-title {
  text-align: center;
  font-size: 60pt;
  font-weight: bolder;
  color: lightcoral;
  margin-bottom: 5px;
}
</style>
