<template>
  <div class="flex flex-col">
    <app-todo-item
      v-for="(item, index) in todos"
      :key="index"
      :text="item.text"
      :isDone="item.isDone"
    />
  </div>
</template>
<script>
import appTodoItem from "./appTodoItem.vue";
export default {
  props: {
    currentCategory: {
      type: String,
      default: "All",
    },
    todos: {
      type: Array,
      required: true,
    },
  },
  components: {
    appTodoItem,
  },
};
</script>
