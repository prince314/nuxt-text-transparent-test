<template>
  <div class="container" @mousemove="mouseMove">
    <h1 data-text="Hello World!" :style="cssVars">Hello World!</h1>
    <span class="cursor"></span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      textElement: "",
      clientRect: "",
      circle: "",
      x: "",
      y: ""
    };
  },
  computed: {
    cssVars() {
      return {
        "--x": this.x,
        "--y": this.y
      };
    }
  },
  mounted() {
    this.textElement = document.querySelector("h1");
    this.clientRect = this.textElement.getBoundingClientRect();
    this.circle = document.querySelector(".cursor");
    this.body = document.querySelector("body");
  },
  methods: {
    mouseMove(event) {
      this.circle.style.left = event.clientX + "px";
      this.circle.style.top = event.clientY + "px";
      this.x = event.clientX - this.clientRect.left + "px";
      this.y = event.clientY - this.clientRect.top + "px";
    }
  }
};
</script>

<style>
body {
  cursor: none;
  background-image: url("../assets/images/background-image.jpg");
}
.container {
  width: 100%;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
h1 {
  font-size: 160px;
  color: #000;
  display: inline-block;
  margin: 50px;
  text-align: center;
  position: relative;
  background: radial-gradient(
    35px circle at var(--x) var(--y),
    rgba(0, 0, 0, 0) 100%,
    black
  );
  background-clip: text;
  -webkit-text-fill-color: transparent;
}
h1:before {
  position: absolute;
  top: 0;
  left: 0;
  content: attr(data-text);
  color: #fff;
  clip-path: circle(35px at var(--x, -100%) var(--y, -100%));
  -webkit-text-stroke-width: 1px;
  -webkit-text-stroke-color: #777;
}
.cursor {
  position: fixed;
  width: 70px;
  height: 70px;
  background: transparent;
  border-radius: 50%;
  border: 1px solid #000000;
  top: 0;
  left: 0;
  transform: translate(-50%, -50%);
}
</style>
