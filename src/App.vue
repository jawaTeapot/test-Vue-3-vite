<template>
  <div class="container">
    <HelloWorld />
  </div>
</template>

<script setup>
import HelloWorld from "./components/HelloWorld.vue";
</script>

<style lang="scss">
body {
  font-family: "Fira Sans", sans-serif;
}
.container {
  width: 1380px;
  margin: 0 auto;
  padding: 0;
}
.btn {
  display: flex;
  align-items: center;
  border: none;
  outline: none;
  border-radius: 50px;
  background-color: transparent;
  cursor: pointer;
}
</style>
