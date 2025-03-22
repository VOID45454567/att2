<template>
  <button :class="`border-2 w-1/3 rounded-xl font-bold transition duration-300 hover:cursor-pointer ${isActive
      ? 'bg-rose-700 text-white border-rose-700'
      : 'border-rose-700 text-rose-700 hover:bg-rose-700 hover:text-white '
    }`">
    {{ text }}
  </button>
</template>

<script>
export default {
  props: {
    text: String,
    isActive: {
      type: Boolean,
      required: true,
    },
  },
};
</script>
