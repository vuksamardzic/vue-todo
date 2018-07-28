<template>
  <form class="form-row pt-2 pb-4"
        @submit.prevent="onSubmit">
    <div class="col">
      <input type="text"
             placeholder="name"
             class="form-control"
             v-model="name"
             title="create todo"></div>
    <div class="col-auto">
      <button class="btn btn-primary ml-2"
              type="submit">create
      </button>
    </div>
  </form>
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'todo-form',
    data() {
      return {
        name: ''
      };
    },
    methods: {
      onSubmit() {
        if (this.name !== '') {
          axios.post('http://localhost:3000/api/v1/todo', { name: this.name })
            .then(() => {
              this.name = '';
              this.$emit('refresh-todo');
            });
        }
      }
    }
  };
</script>

<style scoped>

</style>
