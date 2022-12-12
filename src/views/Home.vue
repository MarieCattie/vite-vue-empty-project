<template lang="">
    <main class="home-page">
        <h1>Home</h1>
        <p>This is home page</p>
        <div>
            <input v-model="getText" />
        </div>
        <div id="coin">
          <UploadImage />
          <div class="circle-wrapper">
            <p class="circle"></p>
            <div class="circle-image">
                <img src="img/coin.png"  alt="">
            </div>
        </div>
        </div>
        
        
        
        <button @click="makeOrder">Создать заказ</button>
        <div class="d-none">{{myVal}}</div>
        <div id="result"></div>
    </main>
</template>

<style lang="scss">
.circle-wrapper {
  width: 300px;
  height: 300px;
  position: relative;
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
.d-none {
  display: none;
}
</style>

<script>
// import { ref } from "vue";
// import { computed } from "vue";


// let getText = ref("hELLO");

// const myVal = computed({
//   get() {
//     if (document.querySelector(".circle")) {
//       document.querySelector(".circle").innerHTML =
//         getText.value
//           .split("")
//           .map((e, i) => {
//             const fontSize = 14;
//             const start = Number(
//               (-getText.value.length / 16) * 90
//             );
//             return `<span style="--rot:${
//               start + i * 12
//             }deg; font-size: ${fontSize}px">${e}</span>`;
//           })
//           .join("");
//     }
//     return getText.value;
//   },
//   set(val) {
//     getText.value = val;
//   },
// });

import {ref} from 'vue'
import { computed } from "vue";
import UploadImage from '../components/UploadImage.vue';
    export default {
        data() {
        return {
            getText: "Hello",
            myVal: null
        }
        },
        components: {
          UploadImage
        },
        methods: {
          makeOrder() {
            html2canvas(document.getElementById("coin")).then(function(canvas) {
              let myscreen = canvas;
              document.getElementById("result").appendChild(myscreen);
            })
          }
        },
        computed: {
          myVal() {
            if (document.querySelector(".circle")) {
      document.querySelector(".circle").innerHTML =
        this.getText
          .split("")
          .map((e, i) => {
            const fontSize = 14;
            const start = Number(
              (-this.getText.length / 16) * 90
            );
            return `<span style="--rot:${
              start + i * 12
            }deg; font-size: ${fontSize}px">${e}</span>`;
          })
          .join("");
    }
          return this.getText;
          }
        },

    }
</script>
