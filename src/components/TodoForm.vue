<template>
    <div>
      <form @submit.prevent="handleSubmit" ref="form">
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
      isEdit: {
        type: Boolean,
        default: false,
      },
      edit: {
        type: Object,
        default: () => ({
          id: 0,
          title: '',
          description: '',
          status: '',
        }),
      },
    },
    data() {
      return {
        todo: { 
          id: 0,
          title: '',
          description: '',
          status: 'WAITING',
        },
      };
    },
    methods: {
      handleSubmit() {    
        this.todo.id++;
        this.$emit('submit',  this.todo);
        this.clearForm();
      },
      clearForm() {
        this.todo = { 
          title: '',
          description: '',
          status: '',
        };
      },
    },
    watch: {
    // whenever question changes, this function will run
    edit: function (newVal) {
      this.todo = newVal;
    }
  },
  };
  </script>
  