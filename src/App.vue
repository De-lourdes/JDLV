<template>
  <div id="app">
    <game-of-life></game-of-life>
  </div>
</template>

<script>
import GameOfLife from '@/components/GameOfLife.vue'; // Assurez-vous que le chemin est correct

export default {
  name: 'App',
  components: {
    GameOfLife // Enregistrez le composant pour qu'il soit utilisable dans ce template
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
