<template>
  <div>
    <div class="menu" v-if="!exit">
      <h1>The Pong Game</h1>
      <div class="btns">
        <button @click="startGame">NOWA GRA</button>
        <button @click="exit=true">WYJŚCIE Z GRY</button>
      </div>
    </div>
    <div class="menu" v-if="exit">
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
h1 {
  font-size: 40px;
}

.btns {
  display: flex;
}

.goodBye {
  font-size: 30px;
}
</style>
