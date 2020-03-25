<template>
  <div>
    <div class="c-cb">
      <input type="checkbox" :id="id" :checked="isCompleted" />
      <label :for="id">{{ name }}</label>
    </div>
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
