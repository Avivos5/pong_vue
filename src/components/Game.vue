<template>
  <canvas id="canv" v-bind:height="canvasHeight" v-bind:width="canvasWidth"></canvas>
</template>


<script>
export default {
  name: "Game",

  props: ["canvasWidth", "canvasHeight"],

  data() {
    return {
      vueCanvas: null,
      // Ball object
      ball: {
        x: this.canvasWidth / 2,
        y: this.canvasHeight / 2,
        radius: 10,
        velocityX: 5,
        velocityY: 5,
        speed: 7,
        color: "#fff",
      },

      // Paddle object
      user: {
        x: 15,
        y: (this.canvasHeight - 100) / 2,
        width: 15,
        height: 100,
        score: 0,
        color: "#fff",
      },

      // NET object
      net: {
        x: (this.canvasWidth - 2) / 2,
        y: 5,
        height: 10,
        width: 2,
        color: "#fff",
      },
    };
  },

  mounted() {
    const canv = document.getElementById("canv");
    const ctx = canv.getContext("2d");
    this.vueCanvas = ctx;
    // console.log(canv);
    // console.log(this.vueCanvas);

    this.render();
  },

  methods: {
    drawRect(x, y, w, h, color) {
      this.vueCanvas.fillStyle = color;
      this.vueCanvas.fillRect(x, y, w, h);
    },

    // draw ball
    drawArc(x, y, r, color) {
      this.vueCanvas.fillStyle = color;
      this.vueCanvas.beginPath();
      this.vueCanvas.arc(x, y, r, 0, Math.PI * 2, true);
      this.vueCanvas.closePath();
      this.vueCanvas.fill();
    },

    // draw the net
    drawNet() {
      for (let i = 0; i <= this.canvasHeight; i += 20) {
        this.drawRect(
          this.net.x,
          this.net.y + i,
          this.net.width,
          this.net.height,
          this.net.color
        );
      }
    },

    render() {
      // draw canvas
      this.drawRect(0, 0, this.canvasWidth, this.canvasHeight, "#000");

      // draw the net
      this.drawNet();

      // draw the user's paddle
      this.drawRect(
        this.user.x,
        this.user.y,
        this.user.width,
        this.user.height,
        this.user.color
      );

      // draw the ball
      this.drawArc(this.ball.x, this.ball.y, this.ball.radius, this.ball.color);
    },
  },
};
</script>

<style scoped>
#canv {
  border: 1px solid black;
}
</style>