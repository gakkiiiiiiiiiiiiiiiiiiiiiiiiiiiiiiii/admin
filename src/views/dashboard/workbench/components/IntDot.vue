<template>
  <div class="relative w-400px h-400px">
    <div
      v-for="(d, i) in dots"
      class="dot"
      :key="i"
      :class="{ checked: props.checked }"
      :style="{ left: `${d.x}px`, top: `${d.y}px` }"
    >
      <div class="ink-dot"> </div>
    </div>
  </div>
</template>

<script setup>
  import { computed } from 'vue'

  const props = defineProps({
    num: Number,
    checked: Boolean,
  })
  function getRandomNumber() {
    return Math.floor(Math.random() * 301)
  }
  const dots = computed(() => {
    return Array.from({ length: props.num }).map((_) => {
      return {
        x: getRandomNumber(),
        y: getRandomNumber(),
      }
    })
  })
</script>

<style>
  .dot {
    position: absolute;
    border-radius: 50%;
  }

  .ink-dot {
    position: absolute;
    width: 10px;
    height: 10px;
    margin-left: -5px;
    margin-top: -5px;
    background-color: black;
    filter: blur(3px);
  }

  .checked {
    padding: 12px;
    border: 1px solid red;
  }
</style>
