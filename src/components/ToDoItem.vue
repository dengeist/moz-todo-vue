<template>
  <div class="stack-small">
    <div class="c-cb">
      <input
        type="checkbox"
        :id="id"
        :checked="isCompleted"
        @change="$emit('toggle-checkbox', id)"
      />
      <label :for="id">{{ name }}</label>
    </div>
    <div class="btn-group">
      <button type="button" class="btn">
        <span>Edit </span>
        <span class="visually-hidden">Eat</span>
      </button>
      <button type="button" class="btn btn__danger">
        <span>Delete </span>
        <span class="visually-hidden">Eat</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isCompleted: this.completed,
      isEditing: false
    };
  },
  props: {
    id: { required: true, type: String },
    name: { required: true, type: String },
    completed: { default: false, type: Boolean }
  }
};
</script>
