<template>
    <div class="todo-item">
      <template v-if="!editing">
        <input type="checkbox" v-model="todo.done">
        <span :class="{ 'done': todo.done }">{{ todo.label }}</span>
        <button @click="editMode" class="edit-btn">Edit</button>
        <button @click="deleteTodo" class="delete-btn">Delete</button>
      </template>
      <template v-else>
        <input type="text" v-model="editedLabel" @keyup.enter="saveEdit" @keyup.esc="cancelEdit">
        <button @click="saveEdit">Save</button>
        <button @click="cancelEdit">Cancel</button>
      </template>
    </div>
  </template>
  
  <script>
  export default {
    props: ['todo'],
    data() {
      return {
        editing: false,
        editedLabel: this.todo.label
      };
    },
    methods: {
      editMode() {
        this.editing = true;
      },
      saveEdit() {
        if (this.editedLabel.trim() !== '') {
          this.$emit('edit', { ...this.todo, label: this.editedLabel });
          this.editing = false;
        }
      },
      cancelEdit() {
        this.editing = false;
      },
      deleteTodo() {
        this.$emit('delete', this.todo.id);
      }
    }
  };
  </script>
  
  <style>

  .todo-item {
  margin-top: 35px;
  margin-bottom: 10px;;
  background-color: pink;
  }

 .todo-item button {
  margin-left: 10px;
 } 

  .done {
    text-decoration: line-through;
  }

  .delete-btn {
  background-color: red; 
  color: white; 
  border: none; 
  padding: 0.5rem 1rem; 
  cursor: pointer; 
  margin-left: 1.0 rem; 
}

  .delete-btn:hover {
  background-color: darkred;
}

 .edit-btn {
  background-color: grey; /* Set warna latar belakang menjadi merah */
  color: white; /* Set warna teks menjadi putih */
  border: none; /* Hapus border */
  padding: 0.5rem 1rem; /* Sesuaikan padding jika perlu */
  cursor: pointer; /* Ubah kursor saat diarahkan */
  margin-left: 1.0 rem; /* Sesuaikan jarak dari tombol sebelumnya */
}

.edit-btn:hover {
  background-color: darkgrey;
}

  </style>
  