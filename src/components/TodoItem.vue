<template>
  <div :class="statusClass" class="p-3 mb-3 text-white">
    <h5>{{ todo.title }}</h5>
    <p>{{ todo.description }}</p>
    <button @click="$emit('edit', todo)" class="btn btn-light">Edit</button>
  </div>
</template>

<script>
export default {
  props: {
    todo: Object,
  },
  computed: {
    statusClass() {
      switch (this.todo.status) {
        case 'WAITING':
          return 'bg-danger';
        case 'IN PROGRESS':
          return 'bg-warning';
        case 'COMPLETED':
          return 'bg-success';
        default:
          return 'bg-secondary';
      }
    },
  },
};
</script>
