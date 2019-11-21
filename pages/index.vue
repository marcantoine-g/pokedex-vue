<template>
  <div class="container">
    <Home/>
    <MainPage/>
  </div>
</template>

<script>
import Home from '@/components/Home.vue';
import MainPage from '@/components/MainPage.vue';

export default {
  components: {
    Home,
    MainPage
  }
}
</script>

<style>
.container {
  min-height: 100vh;
  font-family: 'Rambla', sans-serif;
}
html{
  scroll-behavior: smooth;
}


</style>
