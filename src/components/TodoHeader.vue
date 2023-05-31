<script setup>
import { RouterLink } from "vue-router";
</script>

<template>
  <div>
    <header>
      <nav class="container">
        <div class="branding">
          <img src="../assets/logo-todos.png" alt="" />
          <h1>Vue Todos</h1>
        </div>
        <ul class="nav-routes">
          <RouterLink to="/">Home</RouterLink>
          <RouterLink to="/about">About</RouterLink>
        </ul>
      </nav>
    </header>
  </div>
</template>

<style lang="scss" scoped>
header {
  background-color: #f1f1f1;
  nav {
    display: flex;
    align-items: center;
    padding: 25px 16px;

    .branding {
      display: flex;
      align-items: center;
      gap: 8px;
      img {
        max-width: 150px;
      }
      h1 {
        font-size: 30px;
      }
    }
    .nav-routes {
      display: flex;
      flex: 1;
      justify-content: flex-end;
      list-style: none;
      gap: 12px;

      a {
        text-decoration: none;
        color: inherit;
      }
    }
  }
}
</style>
