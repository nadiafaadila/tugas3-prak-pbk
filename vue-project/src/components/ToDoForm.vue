<template>
    <div>
      <input type="text" v-model="label" @keyup.enter="addToDo">
      <button @click="addToDo">Add</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        label: ''
      };
    },
    methods: {
      addToDo() {
        if (this.label.trim() !== '') {
          this.$emit('todo-added', this.label);
          this.label = '';
        }
      }
    }
  };
  </script>
  