<template>
  <div class="flex flex-col mx-auto w-1/3 border-2 border-rose-600 rounded-md p-4 mb-5">
    <div class="flex flex-row w-5/6 mx-auto gap-5">
      <app-button v-for="category in categories" :key="category" :text="category"
        :isActive="currentCategory === category" @click="setCurrentCategory(category)" />
    </div>
    <!-- Контейнер для списка дел с анимацией -->
    <div ref="todoListRef" class="flex flex-col">
      <app-todo-item v-for="(item, index) in filteredTodos" :key="item.text" :text="item.text" :isDone="item.isDone" />
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
    const todoListRef = ref(null); // Ссылка на контейнер списка дел

    // Инициализация AutoAnimate после монтирования компонента
    onMounted(() => {
      if (todoListRef.value) {
        autoAnimate(todoListRef.value); // Применяем AutoAnimate к контейнеру
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
