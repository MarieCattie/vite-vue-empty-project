<template lang="">
    <main class="home-page">
        <h1>Home</h1>
        <p>This is home page</p>
        <div>
            <input v-model="getText" />
        </div>
        <div class="circle-wrapper">
            <p class="circle"></p>
            <div class="circle-image">
                <img src="img/coin.png"  alt="">
            </div>
        </div>
        <div class="d-none">{{myVal}}</div>
    </main>
</template>

<style lang="scss">
.circle-wrapper {
  width: 300px;
  height: 300px;
  position: relative;
  margin: 0px auto;
  .circle {
    position: absolute;
    width: 107px;
    height: 107px;
    border-radius: 50%;
    background: transparent;
    text-align: center;
    line-height: 200px;
    font-size: 22px;
    left: 50px;
    top: 32px;
    color: rgba(0, 0, 0, 1);
    font-weight: bolder;
    
    span {
      display: inline-block;
      width: 120px;
      position: absolute;
      transform: translate(-12.5px, 0px) rotate(var(--rot)) translate(0, -63px);
      text-align: center;
      height: 320px;
      top: -39px;
      text-shadow: 0px 2px 1px rgb(255 255 255 / 50%), 0px 1px 0px rgb(255 255 255 / 75%);
    }
  }
}
.circle-image {
  width: 100%;

  img {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }
}
</style>

<script setup>
import { ref } from "vue";
import { computed } from "vue";

let getText = ref("hELLO");

const myVal = computed({
  get() {
    if (document.querySelector(".circle")) {
      document.querySelector(".circle").innerHTML =
        getText.value
          .split("")
          .map((e, i) => {
            const fontSize = 14;
            const start = Number(
              (-getText.value.length / 16) * 90
            );
            return `<span style="--rot:${
              start + i * 12
            }deg; font-size: ${fontSize}px">${e}</span>`;
          })
          .join("");
    }
    return getText.value;
  },
  set(val) {
    getText.value = val;
  },
});
</script>
