<template>
  <div>
    <div class="menu" v-if="!exit">
      <p class="mainText">Koniec gry</p>
      <div class="results">
        <p>Twój wynik: 0</p>
        <p>Najlepszy wynik: 0</p>
      </div>
      <button>ZAGRAJ PONOWNIE</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "EndMenu",
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
