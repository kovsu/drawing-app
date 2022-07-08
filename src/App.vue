<script setup lang="ts">
import { provide, ref } from "vue";
import DrawingContainer from "./components/DrawingContainer.vue";
import HeaderOperation from "./components/HeaderOperation.vue";

let size = ref(1);
let isClear = ref(0);

function change(value: boolean) {
  if (value) {
    size.value += 1;
  } else {
    size.value -= 1;
  }
}

function clear() {
  isClear.value += 1;
}

let defaultColor = ref("#55efc4");

provide("lineColor", defaultColor);

function colorVal(color: string) {
  console.log(color);
  defaultColor.value = color;
}
</script>

<template>
  <HeaderOperation
    :lineWidth="size"
    @change="change"
    @clear="clear"
    @commit-color="colorVal"
  />
  <DrawingContainer :lineWidth="size" :isClear="isClear" />
</template>

<style lang="scss">
@import url("./styles/main.scss");
</style>
