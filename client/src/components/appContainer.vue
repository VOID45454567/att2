<template>
  <div class="flex flex-col mx-auto w-1/3 border-2 border-rose-600 rounded-md p-4 mb-5">
    <div class="flex flex-row w-5/6 mx-auto gap-5">
      <app-button v-for="category in categories" :key="category" :text="category"
        :isActive="currentCategory === category" @click="setCurrentCategory(category)" />
    </div>
    <app-todo-list :todos="filteredTodos" />
  </div>
  <div>
    <app-add-todo />
  </div>
</template>

<script>
import AppButton from "./appButton.vue";
import AppTodoList from "./appTodoList.vue";
import AppAddTodo from "./appAddTodo.vue";
export default {
  components: {
    AppButton,
    AppTodoList,
    AppAddTodo,
  },
  data() {
    return {
      currentCategory: null,
      categories: ["All", "Active", "Done"],
      todos: [
        { text: "aBcDeFgHiJ", isDone: true },
        { text: "kLmNoPqRsT", isDone: false },
        { text: "uVwXyZaBcD", isDone: true },
        { text: "eFgHiJkLmN", isDone: false },
        { text: "oPqRsTuVwX", isDone: true },
        { text: "yZaBcDeFgH", isDone: false },
        { text: "iJkLmNoPqR", isDone: true },
        { text: "sTuVwXyZaB", isDone: false },
        { text: "cDeFgHiJkL", isDone: true },
        { text: "mNoPqRsTuV", isDone: false },
      ],
    };
  },
  methods: {
    setCurrentCategory(category) {
      this.currentCategory = category;
    },
  },
  computed: {
    filteredTodos() {
      if (this.currentCategory === "All") {
        return this.todos;
      } else if (this.currentCategory === "Active") {
        return this.todos.filter((todo) => !todo.isDone);
      } else {
        return this.todos.filter((todo) => todo.isDone);
      }
    },
  },
};
</script>
