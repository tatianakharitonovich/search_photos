<script setup>
import Greetings from './components/Greetings.vue'
import SearchData from './components/SearchData.vue'
</script>

<template>
  <header>
    <img alt="logo" class="logo" src="./assets/images/logo.jpg" width="63" height="80" />
    <div class="wrapper">
      <Greetings msg="Would you like to find interesting photos?" />
    </div>
  </header>
  <main>
    <SearchData />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
