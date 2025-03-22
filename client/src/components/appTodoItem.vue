<template>
  <div
    class="flex flex-row px-5 py-2 w-5/6 border-2 my-2 border-rose-600 mx-auto justify-between items-center rounded-md">
    <div>
      <p class="text-rose-600">{{ text }}</p>
      <p>
        status
        <span class="text-rose-600 font-extrabold">{{
          isDone ? "Done" : "Active"
        }}</span>
      </p>
    </div>

    <button
      class="border-2 px-5 rounded-lg transition duration-300 border-rose-700 text-rose-700 hover:bg-rose-700 hover:text-white ' hover:cursor-pointer">
      Done
    </button>
  </div>
</template>
<script>
export default {
  props: {
    text: {
      type: String,
      default: "",
    },
    isDone: {
      type: Boolean,
      default: false,
    },
  },
};
</script>
<style></style>
