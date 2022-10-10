<template>
  <div class="AccordionButtons">
    <button class="AccordionButtons__btn btn">
      <img src="/vector_5.svg" alt="img" />
    </button>
    <button class="AccordionButtons__btn btn">
      <img src="/delete.svg" alt="img" />
    </button>
    <button class="AccordionButtons__btn btn handle">
      <img src="/vector_6.svg" alt="img" />
    </button>
  </div>
</template>

<script setup></script>

<style lang="scss" scoped>
@import "../assets/variables.scss";
.AccordionButtons {
  display: flex;
  align-items: center;
  &__btn {
    margin-right: 22px;
    width: 15px;
    height: 15px;
    justify-content: center;
    &:last-child {
      margin-right: 0;
    }
  }
}
</style>
