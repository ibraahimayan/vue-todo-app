<template>
    <div class="container">
      <h2 class="my-4">Todo List</h2>
  
      <Form :edit="selectedTodo" :isEdit="isEditMode" @submit="handleFormSubmit" />

      <div class="form-group">
        <label for="filter">Filter by Status</label>
        <select v-model="filterStatus" class="form-control" id="filter">
          <option value="">All</option>
          <option value="WAITING">Waiting</option>
          <option value="IN PROGRESS">In Progress</option>
          <option value="COMPLETED">Completed</option>
        </select>
      </div>
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
        selectedTodo: {
          title: '',
          description: '',
          status: '',
        },
        isEditMode: false,
        filterStatus: '',
      };
    },
    computed: {
      filteredTodos() {
        if (this.filterStatus) {
          return this.todos.filter(todo => todo.status === this.filterStatus);
        }
        return this.todos.filter(todo => todo.status);
      },
    },
    methods: {
      handleFormSubmit(todo) {
        const newTodo = { ...todo };
        if (this.isEditMode) {
          const index = this.todos.findIndex(t => t.id === todo.id);
          if (index !== -1) {
            this.todos.splice(index, 1, todo);
          }
        } else {
          this.todos.push(newTodo);
        }
      },
      editTodo(todo) {
        this.selectedTodo = { ...todo };
        this.isEditMode = true;
      },
      resetForm() {
        this.isEditMode = false;
      },
    },
  };
  </script>
  