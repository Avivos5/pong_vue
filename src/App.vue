<template>
  <div id="app">
    <StartMenu v-if="!gameOn" @startGame="gameOn = true" />
    <Game v-if="gameOn" canvasHeight="500" canvasWidth="1000" />
  </div>
</template>

<script>
import Game from "./components/Game.vue";
import StartMenu from "./components/StartMenu.vue";

export default {
  name: "App",
  components: {
    Game,
    StartMenu,
  },

  data() {
    return {
      gameOn: false,
    };
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap");
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Press Start 2P", cursive;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
