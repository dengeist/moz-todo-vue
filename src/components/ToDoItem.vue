<template>
  <div>
    <input type="checkbox" id="todo-item" :checked="isCompleted" />
    <label for="todo-item">{{ name }}</label>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isCompleted: this.completed
    };
  },
  props: {
    id: { required: true, type: String },
    name: { required: true, type: String },
    completed: { default: false, type: Boolean }
  }
};
</script>
