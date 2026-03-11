<script setup>
import { RouterLink } from "vue-router";
</script>

<template>
  <header>
    <nav class="container">
      <div class="nav-content">
        <img src="../assets/logo.png" alt="Todo List logo" />
        <h1>Todo List</h1>
      </div>
      <ul class="nav-routes">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </ul>
    </nav>
  </header>
</template>

<style lang="scss" scoped>
header {
  background-color: #d6bde0;
  color: rgb(250, 249, 246);
  nav {
    display: flex;
    align-items: center;
    padding: 10px 16px;

    .nav-content {
      display: flex;
      align-items: center;
      gap: 8px;
      img {
        max-width: 70px;
      }

      h1 {
        font-size: 25px;
        text-align: center;
      }
    }

    .nav-routes {
      display: flex;
      flex: 1;
      justify-content: flex-end;
      gap: 12px;
      list-style: none;

      a {
        text-decoration: none;
        color: inherit;
      }
    }
  }
}
</style>
