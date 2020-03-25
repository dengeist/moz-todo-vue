<template>
  <div id="app">
    <h1>TodoMatic</h1>
    <to-do-form @add-todo="addTodo" />
    <ul>
      <li v-for="item in ToDoItems" :key="item.id">
        <to-do-item v-bind="item" />
      </li>
    </ul>
  </div>
</template>

<script>
import nanoid from "nanoid";
import ToDoForm from "./components/ToDoForm";
import ToDoItem from "./components/ToDoItem";

console.dir(nanoid);

export default {
  name: "App",
  components: {
    ToDoItem,
    ToDoForm
  },
  data() {
    return {
      ToDoItems: [
        {
          id: "todo-0",
          name: "Learn Vue",
          completed: false
        },
        {
          id: "todo-1",
          name: "Create a Vue project with the CLI",
          completed: true
        },
        { id: "todo-2", name: "Have fun", completed: true },
        {
          id: "todo-3",
          name: "Create a to-do list",
          completed: false
        }
      ]
    };
  },
  methods: {
    addTodo(name) {
      const newTodo = {
        name,
        id: "todo-",
        completed: false
      };
      this.ToDoItems.push(newTodo);
    }
  }
};
</script>

<style></style>
