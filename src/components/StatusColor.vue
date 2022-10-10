<template>
  <div class="StatusColor">
    <template v-if="props.state === 'mandatory'">
      <div class="StatusColor__ellipse StatusColor__ellipse--pink"></div>
      <div class="StatusColor__ellipse StatusColor__ellipse--yellow"></div>
      <div
        class="StatusColor__ellipse StatusColor__ellipse--orange StatusColor__ellipse--active"
      ></div>
    </template>
    <div
      class="StatusColor__ellipse StatusColor__ellipse--azure"
      v-if="props.state === 'ellipse'"
    ></div>
    <template v-if="props.state === 'contract'">
      <div class="StatusColor__ellipse StatusColor__ellipse--blue"></div>
      <div class="StatusColor__ellipse StatusColor__ellipse--gray"></div>
    </template>
  </div>
</template>

<script setup>
const props = defineProps(["state"]);
</script>

<style lang="scss" scoped>
@import "../assets/variables.scss";
.StatusColor {
  margin-right: 15px;
  display: flex;
  align-items: center;
  &__ellipse {
    margin-right: 6px;
    width: 8px;
    height: 8px;
    border-radius: 50%;
    &:last-child {
      margin-right: 0;
    }
    &--active {
      border: 1px solid $primary-text;
    }
    &--pink {
      background-color: $pink;
    }
    &--yellow {
      background-color: $yellow;
    }
    &--orange {
      background-color: $orange;
    }
    &--azure {
      background-color: $azure;
    }
    &--blue {
      background-color: $border-bottom;
    }
    &--gray {
      background-color: $secondary-text;
    }
  }
}
</style>
