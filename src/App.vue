<template>
  <div id="app" class="todoapp">
    <h1>TodoMatic</h1>
    <to-do-form @add-todo="addTodo" ref="newTodoInput" />
    <h2 id="list-summary">{{ listHeadingText }}</h2>
    <ul
      aria-labelledby="list-summary"
      class="todo-list stack-large stack-exception"
    >
      <li v-for="item in ToDoItems" :key="item.id" class="todo">
        <to-do-item
          v-bind="item"
          @toggle-checkbox="toggleTodoCompleted"
          @delete-todo="deleteTodo"
        />
      </li>
    </ul>
  </div>
</template>

<script>
import nanoid from "nanoid";
import ToDoForm from "./components/ToDoForm";
import ToDoItem from "./components/ToDoItem";

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
  computed: {
    listHeadingText() {
      const completedItemsLength = this.ToDoItems.filter(
        item => !item.completed
      ).length;
      const noun = completedItemsLength !== 1 ? "items" : "item";
      return completedItemsLength + ` ${noun} remaining`;
    }
  },
  methods: {
    addTodo(name) {
      const newTodo = {
        name,
        id: "todo-" + nanoid(),
        completed: false
      };
      this.ToDoItems.push(newTodo);
    },
    toggleTodoCompleted(id) {
      const updatedItem = this.ToDoItems.find(item => item.id === id);
      updatedItem.completed = !updatedItem.completed;
    },
    deleteTodo(id) {
      this.ToDoItems = this.ToDoItems.filter(t => t.id !== id);
      this.$refs.newTodoInput.focus();
    }
  }
};
</script>

<style></style>
