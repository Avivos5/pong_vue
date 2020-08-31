<template>
  <div>
    <div class="menu">
      <p class="mainText">Koniec gry</p>
      <div class="results">
        <p>Twój wynik: {{score}}</p>
        <p>Najlepszy wynik: {{bestScore}}</p>
      </div>
      <button @click="newGame">ZAGRAJ PONOWNIE</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "EndMenu",

  props: ["score", "bestScore"],

  methods: {
    newGame() {
      this.$emit("newGame");
    },
  },
};
</script>

<style scoped>
.results {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.results p {
  margin: 5px 0;
}

.mainText {
  font-size: 30px;
}
</style>
