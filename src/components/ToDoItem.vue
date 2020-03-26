<template>
  <div class="todo stack-small" v-if="!isEditing">
    <div class="c-cb">
      <input
        type="checkbox"
        :id="id"
        :checked="isCompleted"
        @change="$emit('toggle-todo', id)"
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

  <form class="todo stack-small" @submit.prevent="handleSubmit" v-else>
    <div class="form-group">
      <label class="todo-label" :for="id">New name for {{ name }}</label>
      <input
        :id="id"
        class="todo-text"
        type="text"
        v-model.lazy.trim="newName"
        ref="focusTarget"
      />
    </div>
    <div class="btn-group">
      <button type="button" class="btn todo-cancel" @click="isEditing = false">
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
      isEditing: false,
      newName: ""
    };
  },
  props: {
    id: { required: true, type: String },
    name: { required: true, type: String },
    completed: { default: false, type: Boolean }
  },
  methods: {
    handleSubmit() {
      this.$emit("rename-todo", this.id, this.newName);
      this.isEditing = false;
    }
  },
  watch: {
    isEditing() {
      this.$nextTick(() => {
        this.$refs.focusTarget.focus();
      });
    }
  }
};
</script>
