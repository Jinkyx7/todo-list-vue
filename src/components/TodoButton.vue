<script setup></script>

<template>
  <button>
    <slot>this is a button</slot>
  </button>
</template>

<style lang="scss" scoped>
button {
  padding: 8px 35px;
  border: none;
  cursor: pointer;
  background-color: #d6bde0;
  color: white;
  border-radius: 2px;

  &:active {
    background-color: #f9f7fa;
    color: #d6bde0;
  }
}
</style>
