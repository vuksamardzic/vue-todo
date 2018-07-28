<template>
  <div class="d-flex justify-content-between">
    <span :class="{'text-line-through': todo.status === 'complete'}">{{ todo.name }}</span>
    <div>
      <i class="icon-done c-pointer text-primary"
         @click="onStatusChange('complete')"
         v-if="todo.status !== 'complete'"></i>

      <i class="icon-favorite c-pointer mx-1 text-danger"
         @click="onStatusChange('incomplete')"
         v-if="todo.status === 'favourite'"></i>

      <i class="icon-non-favorite c-pointer mx-1 text-danger"
         @click="onStatusChange('favourite')"
         v-if="todo.status === 'incomplete'"></i>

      <i class="icon-delete c-pointer text-secondary"
         @click="deleteTodo()"></i>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'todo',
    props: {
      todo: Object
    },
    methods: {
      onStatusChange(status) {
        this.todo.status = status;
        axios.put(`http://localhost:3000/api/v1/todo/${this.todo.id}`, this.todo)
          .then(() => {
            this.$emit('refresh-todo');
          });
      },
      deleteTodo() {
        axios.delete(`http://localhost:3000/api/v1/todo/${this.todo.id}`)
          .then(() => {
            this.$emit('refresh-todo');
          });
      }
    }
  };
</script>

<style scoped>
  .text-line-through {
    text-decoration: line-through;
  }
</style>
