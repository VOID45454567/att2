<template>
  <div class="mx-auto w-1/3 border-2 border-rose-600 rounded-md p-4">
    <h1 class="text-center text-rose-600 font-bold">Add</h1>
    <input type="text" placeholder="text" class="peer w-full bg-slate-100 p-2 text-center border-rose-600 rounded-md"
      v-model="title" @input="CalcRemainingChars" />
    <p class="mb-5 text-sm">
      Remaning chars: <span class="text-rose-600">{{ remainingChars }}</span>
    </p>
    <button
      class="w-full p-2 text-center text-white bg-rose-600 rounded-md translition duration-300 hover:bg-rose-700 focus:bg-rose-400 hover:cursor-pointer"
      @click="save">
      Add to list
    </button>
    <p class="mt-2 text-pink-600 text-sm" v-if="showMessage">
      Submit your text to add it to the list.
    </p>
  </div>
</template>
<script>
export default {
  data() {
    return {
      showMessage: false,
      remainingChars: 90,
      title: "",
    };
  },
  computed: {
    CalcRemainingChars() {
      this.remainingChars = 90 - this.title.length;
    },
  },
  methods: {
    save() {
      if (this.title.length === 0) {
        this.showMessage = true;
      } else {
        this.title = "";
        this.remainingChars = 90;
        this.showMessage = false;
      }
    },
  },
};
</script>
<style></style>
