<template>
  <img :src="image" alt="heart_icon" class="heart" />
</template>

<script>
import image from "../assets/heart_icon.png";

export default {
  name: "LifeIcon",

  data() {
    return {
      image: image,
    };
  },
};
</script>

<style scoped>
.heart {
  height: 50px;
}
</style>
