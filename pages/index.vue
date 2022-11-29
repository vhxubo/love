<script setup>
import { loadFull } from "tsparticles";
import { loadHeartShape } from "tsparticles-shape-heart";
import gsap from "gsap";
import dayjs from "dayjs";
onMounted(() => {
  const timeLine = gsap.timeline({ repeat: -1 });
  gsap.set("#text-utils-animation", { x: 0, y: 0 });
  timeLine
    .fromTo(
      "#text-utils-animation .right span",
      { y: 100, opacity: 0 },
      { y: 0, opacity: 1, stagger: 1 }
    )
    .to(
      "#text-utils-animation .right span",
      {
        y: -100,
        opacity: 0,
        stagger: 1,
      },
      1
    );
});
</script>

<script>
export default {
  data() {
    return {
      options: {
        background: {
          color: "#FCE7F3",
        },
        particles: {
          number: {
            value: 52,
          },
          move: {
            enable: true,
            speed: { min: 1, max: 3 },
          },
          shape: {
            type: "heart",
          },
          size: {
            value: { min: 10, max: 20 },
          },
          color: {
            value: "#ff0000",
          },
          opacity: {
            value: { min: 0.1, max: 0.3 },
            anim: {
              enable: true,
              speed: 1,
              opacity_min: 0,
              sync: false,
            },
          },
        },
        fullScreen: {
          enable: true,
          zIndex: -1,
        },
      },
    };
  },
  methods: {
    async particlesInit(engine) {
      await loadHeartShape(engine);
      await loadFull(engine);
    },
  },
};
</script>

<template>
  <main>
    <div class="z-10 h-screen flex justify-center pl-32">
      <div
        id="text-utils-animation"
        class="test flex flex-1 flex-col justify-center text-pink-500 text-5xl"
      >
        <div class="flex">
          <div class="left">张宁</div>
          <div class="right">
            <span>爱人</span>
            <span>女友</span>
            <span>老婆</span>
            <span>兄弟</span>
            <span>闺蜜</span>
          </div>
        </div>
      </div>
      <div class="flex flex-1">img</div>
    </div>
    <Particles
      id="tsparticles"
      :particlesInit="particlesInit"
      :options="options"
    />
  </main>
</template>
<style lang="scss">
.left {
  margin-right: 8px;
}
.right {
  display: inline-block;
  position: relative;
  flex: 1;
  span {
    position: absolute;
    top: 0;
    left: 0;
    opacity: 0;
  }
}
</style>
