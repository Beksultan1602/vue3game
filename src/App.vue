<template>
  <div class='app'>
    <img class='logo' alt="game logo" src="./assets/gamelogo.png">
    <h1 class="h1">Remember Me, Vue 3</h1>
    <p>Запомни и открой все белые клетки</p>
    <Board />
  </div>
</template>

<script>
import Board from '@/components/Board'
export default {
  name: 'App',
  components: {
    Board,
  }
}
</script>

<style scoped>
  .app {
    padding-top: 30px;
    width: 100%;
    height: 100%;
    background: #000;
    position: fixed;
    top: 0;
    left: 0;
    font-family: Helvetica sans-serif;
    text-align: center;
    color: #f74e00;
  }
  .logo {
    width: 100px;
  }
</style>
