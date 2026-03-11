<template>
  <main>
    <div class="about">
      <h1>About Todo List</h1>
      <p>
        This project is a lightweight todo app built with Vue 3, Vue Router,
        and Vite. It lets you manage tasks in the browser and keeps your list
        saved in local storage between sessions.
      </p>
    </div>
  </main>
</template>

<style lang="scss" scoped>
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;
  color: rgb(51, 49, 49);

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }
}
</style>
