<template>
  <div>
    <h1>Testando a api do Github</h1>
    <Search />
  </div>
</template>

<script>
import Search from './Search.vue'

export default {
  name: "HelloWorld",
  data() {
    return {
    };
  },
  components: {
    Search
  }
}
</script>

<style>
h1 {
  margin-top: 15px;
  text-align: center;
  color: rgb(255, 255, 255);
}

body{
  background-color: rgb(110, 34, 133);
}
</style>
