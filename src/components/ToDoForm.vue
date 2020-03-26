<template>
  <form @submit.prevent="onSubmit">
    <h2 class="label-wrapper">
      <label for="new-todo-input" class="label__lg">
        What needs to be done?
      </label>
    </h2>
    <input
      type="text"
      id="new-todo-input"
      name="new-todo"
      class="input__lg"
      autocomplete="off"
      v-model.lazy.trim="name"
      ref="input"
    />
    <button type="submit" class="btn btn__primary btn__lg">
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
    },
    focus() {
      this.$refs.input.focus();
    }
  }
};
</script>
