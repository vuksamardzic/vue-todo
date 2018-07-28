<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-12">
          <h3 class="mt-2">vue todo</h3>
          <small class="text-info">simple project made in vue.js (<a href="https://github.com/vuksamardzic/vue-todo">source code</a>)</small>
          <todo-form @refresh-todo="execGetTodos"/>
          <p v-if="!data.length"
             class="small">Your todo list looks empty, let's add some :)</p>
          <ul class="list-group list-group-flush">
            <li class="list-group-item"
                v-for="(i, index) in data"
                :class="{'bt-0': index === 0}"
                :key="i.id">
              <todo @refresh-todo="execGetTodos"
                    :todo="i"/>
            </li>
          </ul>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
  import 'bootstrap/dist/css/bootstrap.min.css';
  import TodoForm from './components/todo-form';
  import Todo from './components/todo';
  import axios from 'axios';

  export default {
    name: 'app',
    data() {
      return {
        data: []
      };
    },
    methods: {
      execGetTodos() {
        axios.get('http://localhost:3000/api/v1/todo')
          .then(res => {
            this.data = res.data;
          });
      }
    },
    mounted() {
      this.execGetTodos();
    },
    components: { TodoForm, Todo }
  };
</script>

<style>
  .bt-0 {
    border-top: 0 !important;
  }

  .c-pointer {
    cursor: pointer;
  }
</style>
