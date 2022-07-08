<script setup lang="ts">
import { onMounted, watch, withCtx } from "vue";

const props = defineProps<{
  lineWidth: number;
  isClear: number;
}>();

interface Point {
  x: number;
  y: number;
}

function drawLine(ctx: CanvasRenderingContext2D, p1: Point, p2: Point) {
  ctx.beginPath();
  ctx.moveTo(p1.x, p1.y);
  ctx.lineTo(p2.x, p2.y);
  ctx.lineWidth = props.lineWidth;
  ctx.stroke();
}

onMounted(() => {
  const canvas = <HTMLCanvasElement>document.querySelector(".canvas");
  const ctx = canvas.getContext("2d")!;
  let isPressed = false;
  let originPoint: Point = {
    x: 0,
    y: 0,
  };

  canvas.addEventListener("mousedown", (e) => {
    isPressed = true;
    originPoint = {
      x: e.offsetX,
      y: e.offsetY,
    };
    console.log(e);
  });

  canvas.addEventListener("mousemove", (e) => {
    if (isPressed) {
      drawLine(ctx, originPoint, { x: e.offsetX, y: e.offsetY });
      originPoint.x = e.offsetX;
      originPoint.y = e.offsetY;
    }
  });

  canvas.addEventListener("mouseup", () => {
    isPressed = false;
  });

  canvas.addEventListener("mouseleave", () => {
    isPressed = false;
  });

  watch(
    () => props.isClear,
    (val) => {
      ctx.clearRect(0, 0, 600, 600);
    }
  );
});
</script>

<template>
  <canvas class="canvas" width="600" height="600"></canvas>
</template>

<style scoped lang="scss">
.canvas {
  border: 1px solid #000;
}
</style>
