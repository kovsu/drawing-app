<script setup lang="ts">
defineProps<{
  lineWidth: number;
}>();

const emit = defineEmits<{
  (e: "change", stauts: boolean): void;
  (e: "clear"): void;
}>();

function plus() {
  emit("change", true);
}

function minus() {
  emit("change", false);
}

function clear() {
  emit("clear");
}
</script>

<template>
  <header class="draw__header">
    <div class="draw__font">
      <font-awesome-icon
        icon="fa fa-circle-minus"
        class="icon"
        @click="minus"
      />
      <p>{{ lineWidth }}</p>
      <font-awesome-icon icon="fa fa-circle-plus" class="icon" @click="plus" />
    </div>
    <div class="draw__clear">
      <button @click="clear">clear</button>
    </div>
  </header>
</template>

<style scoped lang="scss">
.draw {
  &__header {
    width: 60rem;
    height: 5rem;
    padding: 2rem;
    border: 1px solid transparent;
    // background-color: red;
    display: flex;
    align-items: center;

    .icon {
      cursor: pointer;
      font-size: 2em;
    }
  }

  &__font {
    margin-right: auto;
    display: flex;
    align-items: center;
    gap: 2rem;

    p {
      font-size: 1.8rem;
      font-weight: 700;
    }
  }

  &__clear {
    button {
      padding: 0.5rem 1rem;
    }
  }
}
</style>
