<template>
  <div id="app" class="todoapp">
    <h1>TodoMatic</h1>
    <to-do-form @add-todo="addTodo" />
    <h2 id="list-summary" ref="listHeading">
      {{ listHeadingText }}
    </h2>
    <p v-if="tasks.length === 0">Use the form to add some tasks!</p>
    <ul
      v-else
      aria-labelledby="list-summary"
      class="todo-list stack-large stack-exception"
    >
      <li v-for="item in tasks" :key="item.id">
        <to-do-item
          v-bind="item"
          @toggle-todo="toggleTodoCompleted"
          @delete-todo="deleteTodo"
          @rename-todo="renameTodo"
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
      tasks: [
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
      const completedItemsLength = this.tasks.filter(item => !item.completed)
        .length;
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
      this.tasks = [...this.tasks, newTodo];
    },
    toggleTodoCompleted(id) {
      const updatedItems = this.tasks.map(item => {
        if (item.id === id) {
          item.completed = !item.completed;
        }
        return item;
      });
      this.tasks = updatedItems;
    },
    deleteTodo(id) {
      this.tasks = this.tasks.filter(t => t.id !== id);
      this.focusListHeading();
    },
    renameTodo(id, name) {
      this.tasks = this.tasks.map(item => {
        if (item.id === id) {
          item.name = name;
        }
        return item;
      });
    },
    focusListHeading() {
      const el = this.$refs.listHeading;
      el.setAttribute("tabindex", "-1");
      el.focus();
      el.removeAttribute("tabindex");
    }
  }
};
</script>
