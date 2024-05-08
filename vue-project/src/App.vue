<template>
  <div id="app">
    <h1 class="title">To-Do List</h1>
    <to-do-form @todo-added="addToDo"></to-do-form>
    <h2 class="subtitle">List Summary</h2>
    <p>{{ listSummary }}</p>
    <ul>
      <li v-for="todo in filteredTodos" :key="todo.id">
        <to-do-item
          :todo="todo"
          @delete="deleteToDo"
          @edit="editToDo"
        ></to-do-item>
      </li>
    </ul>
  </div>
  <div class="filter-controls">
  <div class="hide-completed">
    <input type="checkbox" id="hideCompleted" v-model="hideCompleted">
    <label for="hideCompleted">Hide Completed</label>
  </div>
  <div class="show-all">
    <input type="checkbox" id="showAll" v-model="showAll">
    <label for="showAll">Show All</label>
  </div>
  </div>
</template>

<script>
import ToDoForm from "./components/ToDoForm.vue";
import ToDoItem from "./components/ToDoItem.vue";

export default {
  name: "App",
  components: {
    ToDoForm,
    ToDoItem,
  },
  data() {
    return {
      todos: [],
      hideCompleted: false,
    };
  },
  methods: {
    addToDo(label) {
      this.todos.push({
        id: Date.now(),
        label: label,
        done: false,
      });
    },
    deleteToDo(todoId) {
      this.todos = this.todos.filter(todo => todo.id !== todoId);
    },
    editToDo(todo) {
      const index = this.todos.findIndex(item => item.id === todo.id);
      if (index !== -1) {
        this.todos.splice(index, 1, todo);
      }
    }
  },
  computed: {
    listSummary() {
      const completed = this.todos.filter(todo => todo.done).length;
      return `${completed} out of ${this.todos.length} tasks completed`;
    },
    filteredTodos() {
      if (this.hideCompleted) {
        return this.todos.filter(todo => !todo.done);
      }
      return this.todos;
    }
  }
};
</script>

<style>
.hide-completed {
  margin-bottom: 10px;
  text-align: center;
}

.show-all {
  margin-bottom: 10px;
  text-align: center;
}

#app {
  font-family: Arial, sans-serif;
  text-align: center;
  justify-content: center;
  align-items: center;
  height: 80px;
  background-color: pink;
}

.filter-controls {
  display: center;
}
</style>
