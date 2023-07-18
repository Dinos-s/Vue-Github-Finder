<template>
  <Finder />
</template>

<script setup>
import Finder from './components/Finder.vue'
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@200;300;400;500&display=swap');

* {
  font-family: 'Roboto', sans-serif;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

h1 {
  text-align: center;
  font-size: 42px;
  margin-bottom: 20px;
  color: rgb(255, 255, 255);
}

::-webkit-scrollbar {
  width: 5px;
}

::-webkit-scrollbar-track {
  background: #222;
  border-radius: 15px;
}

::-webkit-scrollbar-thumb {
  background: #c50cac;
  border-radius: 15px;
}

::-webkit-scrollbar-thumb:hover {
  background: #faf9f7;
}
</style>
