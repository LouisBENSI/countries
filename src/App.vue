<template>
  <Header/>
  <Main/>
</template>

<script>
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";
export default {
  components: {Main, Header}
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;600;700;800&display=swap');
body {
  font-family: 'Montserrat', sans-serif;
}
</style>