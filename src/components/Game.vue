<template>
  <canvas
    id="canv"
    v-bind:height="canvasHeight"
    v-bind:width="canvasWidth"
    v-on:mousemove="playerPosition($event)"
  ></canvas>
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
        velocityX: -5,
        velocityY: 5,
        startSpeed: 5,
        currentSpeed: 5,
        color: "#fff",
      },

      // Paddle object
      user: {
        x: 10,
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

      intervalId: "",
    };
  },

  mounted() {
    const canv = document.getElementById("canv");
    const ctx = canv.getContext("2d");
    this.vueCanvas = ctx;
    // console.log(canv);
    // console.log(this.vueCanvas);

    // this.render();
    this.game();
  },

  beforeDestroy() {
    clearInterval(this.intervalid1);
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

    playerPosition(e) {
      this.user.y =
        e.clientY - this.vueCanvas.canvas.offsetTop - this.user.height / 2;

      if (this.user.y >= this.canvasHeight - this.user.height) {
        this.user.y = this.canvasHeight - this.user.height;
      }

      if (this.user.y <= 0) {
        this.user.y = 0;
      }
    },

    resetBall() {
      this.ball.x = this.canvasWidth / 2;
      this.ball.y = this.canvasHeight / 2;
      Math.random() > 0.5
        ? (this.ball.velocityY = 5)
        : (this.ball.velocityY = -5);
      this.ball.currentSpeed = this.ball.startSpeed;
    },

    update() {
      if (
        this.ball.y - this.ball.radius < 0 ||
        this.ball.y + this.ball.radius > this.canvasHeight
      ) {
        //when the ball hits top or bottom wall
        this.ball.velocityY = -this.ball.velocityY;
      }

      if (this.ball.x + this.ball.radius > this.canvasWidth) {
        // when the ball hits right wall
        this.ball.velocityX = -this.ball.velocityX;
      }

      if (this.ball.x - this.ball.radius < 0) {
        // when the ball hits left wall
        this.resetBall();
      }

      if (
        this.user.y < this.ball.y + this.ball.radius &&
        this.user.x + this.user.width > this.ball.x - this.ball.radius &&
        this.user.y + this.user.height > this.ball.y - this.ball.radius
      ) {
        // paddle collision handling

        const collPoit = this.ball.y - (this.user.y + this.user.height / 2); //checking part of the paddle which was hit by the ball

        const normCollPoint = collPoit / (this.user.height / 2); //normalising the collision point between -1 and 1

        const angleRadians = (Math.PI / 3) * normCollPoint; //calulating the angle (in this siutation max. angle will be 60 and min -60 degrees)

        this.ball.velocityX = this.ball.currentSpeed * Math.cos(angleRadians);
        this.ball.velocityY = this.ball.currentSpeed * Math.sin(angleRadians);

        this.ball.currentSpeed += this.ball.startSpeed * 0.01;
      }

      this.ball.x += this.ball.velocityX;
      this.ball.y += this.ball.velocityY;
    },

    game() {
      this.intervalId = setInterval(() => {
        this.update();
        this.render();
      }, 1000 / 60); // 60 FPS
    },
  },
};
</script>

<style scoped>
#canv {
  border: 1px solid black;
}
</style>