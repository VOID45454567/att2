<template>
  <div class="flex flex-col mx-auto w-1/3 border-2 border-rose-600 rounded-md p-4 mb-5">
    <div class="flex flex-row w-5/6 mx-auto gap-5">
      <app-button v-for="category in categories" :key="category" :text="category"
        :isActive="currentCategory === category" @click="setCurrentCategory(category)" />
    </div>
    <div v-if="!filteredTodos.length">
      <p class="text-center text-lg text-gray-500">No todos in this category</p>
    </div>
    <div v-else ref="todoListRef" class="flex flex-col">
      <app-todo-item v-for="item in filteredTodos" :key="item.id" :text="item.text" :isDone="item.isDone" :id="item.id"
        @toggle-category="handleToggleCategory" />
    </div>
  </div>
  <div>
    <app-add-todo />
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import autoAnimate from "@formkit/auto-animate";
import AppButton from "./appButton.vue";
import AppTodoItem from "./appTodoItem.vue";
import AppAddTodo from "./appAddTodo.vue";

export default {
  components: {
    AppButton,
    AppTodoItem,
    AppAddTodo,
  },
  setup() {
    const todoListRef = ref(null);

    onMounted(() => {
      if (todoListRef.value) {
        autoAnimate(todoListRef.value);
      }
    });

    return {
      todoListRef,
    };
  },
  data() {
    return {
      currentCategory: "All",
      categories: ["All", "Active", "Done"],
      todos: [
        // { id: 1, text: "aBcDeFgHiJ", isDone: true },
        // { id: 2, text: "kLmNoPqRsT", isDone: false },
        // { id: 3, text: "uVwXyZaBcD", isDone: true },
        // { id: 4, text: "eFgHiJkLmN", isDone: false },
        // { id: 5, text: "oPqRsTuVwX", isDone: true },
        // { id: 6, text: "yZaBcDeFgH", isDone: false },
        // { id: 7, text: "iJkLmNoPqR", isDone: true },
        // { id: 8, text: "sTuVwXyZaB", isDone: false },
        // { id: 9, text: "cDeFgHiJkL", isDone: true },
        // { id: 10, text: "mNoPqRsTuV", isDone: false },
      ],
    };
  },
  methods: {
    setCurrentCategory(category) {
      this.currentCategory = category;
    },
    handleToggleCategory(data) {
      // Если категория "All", удаляем задачу
      if (this.currentCategory === "All") {
        this.todos = this.todos.filter(task => task.id !== data.id);
      }
      // Иначе просто меняем статус
      else {
        const task = this.todos.find(task => task.id === data.id);
        if (task) {
          task.isDone = data.isDone;
        }
      }
    }
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