<template>
  <div id="app">
    <StartMenu v-if="!gameOn" @startGame="gameOn = true" />

    <div class="gameWrapper" v-if="gameOn && 
    !gameFinished">
      <div class="iconsWrapper">
        <LifeIcon v-for="n in gameResult.lifes" :key="n" />
      </div>

      <Game
        v-if="gameOn && !gameFinished"
        canvasHeight="500"
        canvasWidth="1000"
        @minusLife="minusLife"
      />
    </div>

    <EndMenu
      v-if="gameFinished"
      :score="gameResult.score"
      :bestScore="gameResult.bestScore"
      @newGame="newGame"
    />
  </div>
</template>

<script>
import Game from "./components/Game.vue";
import StartMenu from "./components/StartMenu.vue";
import EndMenu from "./components/EndMenu.vue";
import LifeIcon from "./components/LifeIcon.vue";

export default {
  name: "App",
  components: {
    Game,
    StartMenu,
    EndMenu,
    LifeIcon,
  },

  data() {
    return {
      gameOn: false,
      gameFinished: false,

      gameResult: {
        score: 0,
        lifes: 3,
        bestScore: 0,
      },
    };
  },

  methods: {
    minusLife(result) {
      this.gameResult.lifes--;
      if (!this.gameResult.lifes) {
        this.gameResult.score = result;
        if (this.gameResult.score >= this.gameResult.bestScore)
          this.gameResult.bestScore = this.gameResult.score;
        this.gameFinished = true;
      }
    },

    newGame() {
      this.gameResult.score = 0;
      this.gameResult.lifes = 3;
      this.gameFinished = false;
      this.gameOn = true;
    },
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

.gameWrapper {
  display: flex;
  flex-direction: column;
}

.iconsWrapper {
  display: flex;
  justify-content: center;
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
