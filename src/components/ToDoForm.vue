<template>
  <form @submit.prevent="onSubmit">
    <label for="new-todo-input">
      What needs to be done?
    </label>
    <input
      type="text"
      id="new-todo-input"
      name="new-todo"
      autocomplete="off"
      v-model.lazy.trim="name"
    />
    <button type="submit">
      Add
    </button>
  </form>
</template>
<script>
function onSubmit() {
  this.$emit("add-todo", this.name);
}
export default {
  name: "ToDoForm",
  data() {
    return {
      name: ""
    };
  },
  methods: {
    onSubmit
  }
};
</script>
