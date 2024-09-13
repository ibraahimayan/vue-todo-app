<template>
    <div>
      <form @submit.prevent="handleSubmit">
        <div class="form-group">
          <label>Title</label>
          <input v-model="todo.title" type="text" class="form-control" placeholder="Enter title" />
        </div>
  
        <div class="form-group">
          <label>Description</label>
          <textarea v-model="todo.description" class="form-control" placeholder="Enter description"></textarea>
        </div>
  
        <div class="form-group">
          <label>Status</label>
          <select v-model="todo.status" class="form-control">
            <option value="WAITING">Waiting</option>
            <option value="IN PROGRESS">In Progress</option>
            <option value="COMPLETED">Completed</option>
          </select>
        </div>
  
        <button type="submit" class="btn" :class="isEdit ? 'btn-warning' : 'btn-success'">
          {{ isEdit ? 'Edit Todo' : 'Add Todo' }}
        </button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      todoItem: {
        type: Object,
        default: () => ({
          title: '',
          description: '',
          status: 'WAITING',
        }),
      },
      isEdit: {
        type: Boolean,
        default: false,
      },
    },
    data() {
      return {
        todo: { ...this.todoItem },
      };
    },
    methods: {
      handleSubmit() {
        this.$emit('submit', this.todo);
      },
    },
  };
  </script>
  