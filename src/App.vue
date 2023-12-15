<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div>
    <header style="text-align: center; padding: 10px;">
      <img src="/src/NASA_logo.svg.png " alt="Logo" class="logo"/>
      <!-- Agregamos una clase "nav-container" al div que contiene el nav -->
    </header>
    <div class="nav-container">
      <nav>
        <RouterLink to="/">Página 1</RouterLink>
        <RouterLink to="/Pagina2">Página 2</RouterLink>
      </nav>
    </div>

    <RouterView />
  </div>
</template>

<style scoped>

header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  margin-bottom: 2rem;
  width: 200px;
  height: auto;


}

.nav-container {
  width: 100%;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {

    width: 200px; /* Ancho del logo */
    margin: 0 auto; /* Se automaticamente al centro si lo quito se va a izq*/
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: center;
    font-size: 1rem;
    font-style: italic;
    padding: 1rem 0;

  }

  .nav-container {
    position: static;
  }
}
</style>