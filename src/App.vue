<template>
  <div id="app">
    <StartMenu v-if="!gameOn" @startGame="gameOn = true" />
    <Game v-if="gameOn" canvasHeight="500" canvasWidth="1000" />
    <EndMenu v-if="gameFinished" />
  </div>
</template>

<script>
import Game from "./components/Game.vue";
import StartMenu from "./components/StartMenu.vue";
import EndMenu from "./components/EndMenu.vue";

export default {
  name: "App",
  components: {
    Game,
    StartMenu,
    EndMenu,
  },

  data() {
    return {
      gameOn: false,
      gameFinished: false,
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

.menu {
  height: 40vh;
  width: 80vh;
  background: black;
  color: white;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
}

button {
  width: 220px;
  height: 70px;
  border: 3px dashed white;
  background: black;
  color: white;
  margin: 0 15px;
  font-family: "Press Start 2P", cursive;
  font-size: 17px;
  cursor: pointer;
  line-height: 25px;
  outline: none;
}
</style>
