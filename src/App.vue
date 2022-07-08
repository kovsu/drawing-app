<script setup lang="ts">
import { ref } from "vue";
import DrawingContainer from "./components/DrawingContainer.vue";
import HeaderOperation from "./components/HeaderOperation.vue";

let size = ref(12);
let isClear = ref(0);

function change(value: boolean) {
  if (value) {
    size.value += 1;
  } else {
    size.value -= 1;
  }
}

function clear() {
  isClear.value +=1;
}

</script>

<template>
  <HeaderOperation :lineWidth="size" @change="change" @clear="clear" />
  <DrawingContainer :lineWidth="size" :isClear="isClear" />
</template>

<style lang="scss">
@import url("./styles/main.scss");
</style>
