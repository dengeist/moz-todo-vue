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

  <form class="stack-small" v-else>
    <div class="form-group">
      <label class="todo-label" for="task-0">New name for Eat</label
      ><input id="task-0" class="todo-text" type="text" value="" />
    </div>
    <div class="btn-group">
      <button type="button" class="btn todo-cancel">
        Cancel<span class="visually-hidden">renaming Eat</span></button
      ><button type="submit" class="btn btn__primary todo-edit">
        Save<span class="visually-hidden">new name for Eat</span>
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
  }
};
</script>
