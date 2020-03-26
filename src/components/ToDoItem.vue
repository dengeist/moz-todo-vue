<template>
  <div class="stack-small" v-if="!isEditing">
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
      <button
        type="button"
        class="btn"
        @click="isEditing = true"
        ref="focusTarget"
      >
        <span>Edit </span>
        <span class="visually-hidden">{{ name }}</span>
      </button>
      <button
        type="button"
        class="btn btn__danger"
        @click="$emit('delete-todo', id)"
      >
        <span>Delete </span>
        <span class="visually-hidden">{{ name }}</span>
      </button>
    </div>
  </div>

  <form class="stack-small" v-else>
    <div class="form-group">
      <label class="todo-label" :for="id">New name for {{ name }}</label>
      <input :id="id" class="todo-text" type="text" />
    </div>
    <div class="btn-group">
      <button
        type="button"
        class="btn todo-cancel"
        @click="isEditing = false"
        ref="focusTarget"
      >
        <span>Cancel </span>
        <span class="visually-hidden">renaming {{ name }}</span>
      </button>
      <button type="submit" class="btn btn__primary todo-edit">
        <span>Save </span>
        <span class="visually-hidden">new name for {{ name }}</span>
      </button>
    </div>
  </form>
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
  },
  watch: {
    isEditing() {
      this.$nextTick(() => {
        this.$refs.focusTarget.focus();
      });
    }
  },
  updated() {
    console.log(this.$props.name + " updated");
  }
};
</script>
