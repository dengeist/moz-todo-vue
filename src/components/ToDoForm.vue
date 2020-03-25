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
export default {
  name: "ToDoForm",
  data() {
    return {
      name: ""
    };
  },
  methods: {
    onSubmit() {
      if (this.name === "") {
        return;
      }
      this.$emit("add-todo", this.name);
      this.name = "";
    }
  }
};
</script>
