<template>
  <div
    class="todo my-3 d-flex justify-content-between"
    @mouseover="hover = true"
    @mouseleave="hover = false"
  >
    <div class="my-2 px-2">{{ description }}</div>
    <div class="mt-2 px-2 d-flex">
      <i
        class="material-icons mx-1"
        v-if="hover || isTouchEnabled()"
        @click="this.$emit('remove', this.index)"
      >
        clear
      </i>

      <i
        class="material-icons"
        @click="this.$emit('toggleCompleted', this.index)"
      >
        {{ isCompleted ? "check_box" : "check_box_outline_blank" }}
      </i>
    </div>
  </div>
</template>

<script>
export default {
  name: "Todo",

  data() {
    return {
      hover: false,
    };
  },

  methods: {
    isTouchEnabled() {
      {
        return (
          "ontouchstart" in window ||
          navigator.maxTouchPoints > 0 ||
          navigator.msMaxTouchPoints > 0
        );
      }
    },
  },

  props: {
    description: String,
    isCompleted: Boolean,
    index: Number,
  },
};
</script>