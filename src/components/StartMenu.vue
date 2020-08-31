<template>
  <div>
    <div class="startMenu" v-if="!exit">
      <h1>The Pong Game</h1>
      <div class="btns">
        <button @click="startGame()">NOWA GRA</button>
        <button @click="exit=true">WYJŚCIE Z GRY</button>
      </div>
    </div>
    <div class="startMenu" v-if="exit">
      <p class="goodBye">Do widzenia :)</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "StartMenu",

  data() {
    return {
      exit: false,
    };
  },

  methods: {
    startGame() {
      this.$emit("startGame");
    },
  },
};
</script>

<style scoped>
.startMenu {
  height: 40vh;
  width: 80vh;
  background: black;
  color: white;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
}

h1 {
  font-size: 40px;
}

.btns {
  /* width: 50%;
  background: yellow; */
  display: flex;
}

button {
  width: 220px;
  height: 70px;
  /* padding: 20px 15px; */
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

.goodBye {
  font-size: 30px;
}
</style>
