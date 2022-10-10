<template>
  <div class="accordion">
    <div @click="isShow = !isShow">
      <slot name="top"></slot>
    </div>
    <div v-show="isShow">
      <slot></slot>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
const isShow = ref(false);
</script>

<style lang="scss" scoped>
@import "../assets/variables.scss";
.accordion {
  width: 1190px;
}
</style>
