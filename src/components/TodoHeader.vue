<script setup>
import { RouterLink } from "vue-router";
</script>

<template>
  <div>
    <header>
      <nav class="container">
        <div class="branding">
          <RouterLink to="/"><h1>リスト Risuto</h1></RouterLink>
        </div>
      </nav>
    </header>
  </div>
</template>

<style lang="scss" scoped>
header {
  background-color: #f1f1f1;
  nav {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 25px 16px;

    .branding {
      display: flex;
      align-items: center;
      gap: 8px;
      a {
        text-decoration: none;
        color: inherit;
      }
      img {
        max-width: 150px;
      }
      h1 {
        margin: 0;
        font-size: 50px;
        font-family: "Bebas Neue", sans-serif;
      }
    }
    .nav-routes {
      display: flex;
      list-style: none;
      justify-content: center;
      gap: 12px;
      font-family: "Bebas Neue", sans-serif;
      font-size: 25px;

      a {
        text-decoration: none;
        color: inherit;
      }
    }
  }
}
</style>
