<template>
    <div class="container">
      <h2 class="my-4">Todo List</h2>
  
      <div class="form-group">
        <label for="filter">Filter by Status</label>
        <select v-model="filterStatus" class="form-control" id="filter">
          <option value="">All</option>
          <option value="WAITING">Waiting</option>
          <option value="IN PROGRESS">In Progress</option>
          <option value="COMPLETED">Completed</option>
        </select>
      </div>
  
      <Form :todoItem="selectedTodo" :isEdit="isEditMode" @submit="handleFormSubmit" />
  
      <div v-for="todo in filteredTodos" :key="todo.id">
        <TodoItem :todo="todo" @edit="editTodo" />
      </div>
    </div>
  </template>
  
  <script>
  import Form from './TodoForm.vue';
  import TodoItem from './TodoItem.vue';
  
  export default {
    components: { Form, TodoItem },
    data() {
      return {
        todos: [],
        selectedTodo: null,
        isEditMode: false,
        filterStatus: '',
      };
    },
    computed: {
      filteredTodos() {
        if (this.filterStatus) {
          return this.todos.filter(todo => todo.status === this.filterStatus);
        }
        return this.todos;
      },
    },
    methods: {
      handleFormSubmit(todo) {
        if (this.isEditMode) {
          const index = this.todos.findIndex(t => t.id === todo.id);
          if (index !== -1) {
            this.todos.splice(index, 1, todo);
          }
        } else {
          todo.id = Date.now();
          this.todos.push(todo);
        }
        this.resetForm();
      },
      editTodo(todo) {
        this.selectedTodo = { ...todo };
        this.isEditMode = true;
      },
      resetForm() {
        this.selectedTodo = null;
        this.isEditMode = false;
      },
    },
  };
  </script>
  