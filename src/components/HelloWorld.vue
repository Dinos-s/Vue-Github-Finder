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

<style scoped></style>
