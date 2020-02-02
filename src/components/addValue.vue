<template>
  <div>
    <form @submit.prevent="addTodo">
      <input type="time" v-model="title" name="title" placeholder="Add value...">
      <input type="submit" value="Submit" class="btn">
    </form>
  </div>
</template>

<script>
// import uuid from 'uuid';
export default {
  name: "AddTodo",
  data() {
    return {
      title: ''
    }
  },
  methods: {
    addTodo() {
      const newTodo = {
        title: this.title,
        completed: false
      }
      // Send up to parent
      this.$emit('add-todo', newTodo);

      this.title = '';
    }
  }
}
</script>

<style scoped>
  form {
    display:grid,flex
  }

  input[type="text"] {
    flex: 10;
    padding: 5px;
    margin-bottom: 5px;
  }

  input[type="submit"] {
    flex: 2;
  }
</style>