<script setup lang="ts">
import { inject, ref } from "vue";

const emit = defineEmits<{
  (e: "colorChange", color: string): void;
}>();

const colors = [
  "#55efc4",
  "#81ecec",
  "#74b9ff",
  "#74b9ff",
  "#a29bfe",
  "#dfe6e9",
  "#00b894",
  "#00cec9",
  "#0984e3",
  "#6c5ce7",
  "#b2bec3",
  "#ffeaa7",
  "#fab1a0",
  "#ff7675",
  "#fd79a8",
  "#636e72",
  "#fdcb6e",
  "#e17055",
  "#d63031",
  "#e84393",
  "#2d3436",
];

let defaultColor = ref(colors[0]);

function changeDefaultColor(index: number) {
  emit("colorChange", colors[index]);
  defaultColor.value = colors[index];
}
</script>

<template>
  <div class="color__container">
    <div class="color__show" :style="`background-color:${defaultColor}`"></div>
    <ul class="color__hidden">
      <li
        class="color__item"
        v-for="(color, index) in colors"
        :key="index"
        :style="`background-color: ${color}`"
        @click="changeDefaultColor(index)"
      ></li>
    </ul>
  </div>
</template>

<style scoped lang="scss">
.color {
  &__container {
    position: relative;
    margin: 2rem;
    padding: 0.2rem;
    border: 1px solid #4d4d4d;
    cursor: pointer;

    &:hover .color__hidden {
      opacity: 1;
      visibility: visible;
    }
  }

  &__show {
    width: 2rem;
    height: 2rem;
  }

  &__hidden {
    opacity: 0;
    visibility: hidden;
    position: absolute;
    width: 30rem;
    height: 10rem;
    background-color: #fff;
    border-radius: 5px;
    box-shadow: 0 5px 10px rgba($color: #000000, $alpha: 0.3);
    list-style: none;
    bottom: 150%;
    left: 50%;
    transform: translate(-50%, 0%);
    padding: 1rem;
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;

    li {
      width: 2rem;
      height: 2rem;
    }

    &::after {
      content: "";
      position: absolute;
      width: 0;
      height: 0;
      border-top: 2rem solid #fff;
      border-right: 2rem solid transparent;
      border-bottom: 2rem solid transparent;
      border-left: 2rem solid transparent;
      bottom: -3rem;
      left: 50%;
      transform: translateX(-50%);
    }
  }
}
</style>
