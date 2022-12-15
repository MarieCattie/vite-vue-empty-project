<template lang="">
    <main class="home-page">
      
      <div class="constructor-head">
        <div>
          <h1>Конструктор монет</h1>
          <p class="posttitle">Создайте уникальный дизайн и оформите заказ</p>
        </div>
        <button class="make-order btn" @click="makeOrder"> <p>Создать заказ</p></button>
      </div>
       
        <div class="constructor">
          <div class="constructor__side constructor__workarea">
            <div class="constructor__image-type">
              <div @click="setGraving" :class="{'active': type.graving}">Гравировка</div>
              <div @click="setColorPrint" :class="{'active': type.colorPrint}">Цветная печать</div>
              <!-- <div>3</div> -->

            </div>
            <div id="coin">
              <UploadImage :width="100" :previewImage="previewImage" />
              <div class="circle-wrapper">
                <p class="circle"></p>
                <div class="circle-image">
                    <img ref="constructorImage" v-bind:src="photo"  alt="">
                </div>
            </div>
            </div>
            <div :class="{'hide': isHideResult}" class="modal-wrapper">
              <div class="modal-wrapper__content">
                <a @click="modalClose" class="modal-wrapper__close material-icons">close</a>
                <div :class="{'hide': isHideResult}" ref="result" id="result">
                  <div class="image-preview image-preview--result"></div>
                  <div class="circle-wrapper">
                    <p class="circle"></p>
                    <div class="circle-image">
                      <img v-bind:src="photo"  alt="">
                    </div>
                </div>
                </div>
                <p>Заказ оформлен</p>
              </div>
            </div>
            
          </div>
          <div class="constructor__side constructor__settings">
            <div class="settings-block">
              <div class="settings-block__group">
                <p class="settings-block__label">Текст на монете</p>
                <input class="settings-block__field" v-model="getText" />
              </div>
              <div class="settings-block__group">
                <p class="settings-block__label">Размер шрифта</p>
                <input class="settings-block__field" v-model="getSize" type="number" />
              </div>
              
          </div>
          <div class="settings-block">
            <div>
              <p class="settings-block__label">Изображение на монете</p>
              <input class="settings-block__field" ref="fileUploaded" type="file" @input="onFileSelected">
           </div>
            
        </div>
        <div class="settings-block settings-block--fixsize">
          <div class="settings-block__variantes">
            <div :class="{'active': design.silver}" @click="setSilver"> <img src="img/coin.png" alt=""> </div>
            <div :class="{'active': design.gold}" @click="setGold"> <img src="img/coin2.png" alt=""> </div>
         </div>
          
      </div>
      <div class="settings-block">
        
          <p class="settings-block__label">Перемещение изображения</p>
          <div class="settings-block__controls">
              <button class="btn material-icons" @click="imageLeft">chevron_left</button>
              <button class="btn material-icons" @click="imageTop">expand_less</button>
              <button class="btn material-icons" @click="imageRight">chevron_right</button>
              <button class="btn material-icons" @click="imageBottom">expand_more</button>
          </div>
    </div>
    <div class="settings-block">
        
      <div class="settings-block__group">
        <p class="settings-block__label">Ширина изображения</p>
        <input class="settings-block__range" type="range" max="1000" min="10" step="1" value="100" @input="changeWidth" />
      </div>
      <div class="settings-block__group">
        <p class="settings-block__label">Высота изображения</p>
        <input class="settings-block__range" type="range" max="1000" min="10" step="1" value="100" @input="changeHeight" />

      </div>
      
</div>
          
          </div>
        </div>
        
        
        <div class="d-none">{{myVal}}</div>

        <div>
          <!-- <img class="result-image"> <canvas></canvas> -->
        </div>
       

       
        <div style="display: none;" id="resultcanvas"></div>
    </main>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.home-page {
  position: relative;
}
.modal-wrapper {
  width: 100vw; height: 100vh;
  z-index: 1000;
  position: fixed;
  top: 0;
  left: 0;
  background-color: rgba(41, 37, 37, 0.342);
  display: flex;
  justify-content: center;
  align-items: center;
  transition: all .5s ease-in;
  &.hide {
    display: none;
  }

  &__close {
    position: absolute;
    right: 20px;
    top: 20px;
    color: red;
    cursor: pointer;
  }

  &__content {
    position: relative;
    width: 400px;
    padding: 30px;
    background-color: #fff;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
}


.settings-block {
  overflow: hidden;
  min-width: 468px;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 5px 6px 10px 0px rgb(193 201 209 / 64%), -2px -1px 8px 3px white;
  border: 1px solid white;
  margin-bottom: 30px;

  &__range {

    width: 100%;
    -webkit-appearance: none !important;
    background: linear-gradient(8.37deg, #FFFFFF -30.86%, #ECF1F7 -10.72%, #CFDCEB 112.31%);
    box-shadow: inset -4px -4px 7px rgba(255, 255, 255, 0.7), inset 4px 4px 6px rgba(18, 46, 101, 0.15);
    border-radius: 31px;
    height:16px;

    &::-webkit-slider-thumb {
      -webkit-appearance: none !important;
      background: linear-gradient(89.72deg, #F0F4F9 -4.95%, #587CA5 578.66%);
      box-shadow: -1px 2px 2px rgba(24, 55, 91, 0.1), inset 0px 0px 4px rgba(46, 68, 87, 0.02), inset 0px -2px 1px rgba(39, 81, 126, 0.12);
      backdrop-filter: blur(14px);
      border-radius: 50%;
      height:33px;
      width:33px;
      cursor: pointer;
    }

  }
  &__controls {
    display: flex;
    align-items: center;

    & .btn {
      color: #fff;

       &:not(:last-of-type) {
      margin-right: 10px;
      
    }
    }
    
   
  }

  &__group {
    margin-bottom: 20px;
  }
  &__variantes {
    max-width: 468px;
    padding: 20px;
    overflow-x: scroll;
    overflow-y: hidden;
    display: flex;
    & div {
      padding: 10px;
      border-radius: 10px;
      width: 200px;
      height: 200px;
      overflow: hidden;
      flex-shrink: 0;
      transition: all .3s ease-in;
      background: var(--light);
      box-shadow: -4px -2px 16px #eaeaeb, 4px 2px 16px rgba(136, 165, 191, 0.48);


      &.active {
        background-color: var(--light);
        box-shadow: inset -3px -3px 7px #ffffff, inset 2px 2px 5px rgb(136 165 191 / 38%);
      }

      &:not(:last-of-type) {
        margin-right: 10px;
      }
      &:hover {
        cursor: pointer;
        box-shadow: 5px 6px 10px 0px rgb(193 201 209 / 64%), -2px -1px 8px 3px rgba(187, 187, 187, 0.712);
      }
      & img {
        width: 100%;
        height: 100%;
        object-fit: contain;
      }
    }
  }
  &__label {
    font-weight: 600;
    color: transparent;
    background: #656b70;
    -webkit-background-clip: text;
    -moz-background-clip: text;
    background-clip: text;
    text-shadow: 0px 3px 3px rgba(255,255,255,0.5);
    margin-bottom: 7px;
  }
}
.settings-block__field {
  font-size: 14px;
  display: block;
  border-radius: 8px;
  outline: none;
  background: 
    linear-gradient(var(--light) 0 0) padding-box, /*this is your grey background*/
    linear-gradient(130.18deg, #FFFFFF 35.92%, rgba(55, 83, 111, 0.4) 190.57%) border-box;
  padding: 5px 16px;
  border: 2px solid transparent;
  box-shadow: inset -3px -3px 7px #FFFFFF, inset 2px 2px 5px rgba(136, 165, 191, 0.38);
  transition: background 0.3s ease;

  &:focus {
    background: 
    linear-gradient(var(--light) 0 0) padding-box, /*this is your grey background*/
    linear-gradient(to right bottom, #F5C21B, #D17000) border-box;
    
}


}
.btn {
  padding: 10px 30px;
  background: -webkit-gradient(linear, left top, left bottom, from(#F5C21B), to(#D17000));
  font-weight: 600;
  color: #F5C21B;
  border-radius: 5px;
  box-shadow: 5px 6px 10px 0px rgb(193 201 209 / 64%), -2px -1px 8px 3px white;

  & p {
    font-weight: 600;
    color: #FFF;
  }
}
.constructor-head {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.constructor {
  padding-top: 20px;
  display: flex;
  justify-content: space-between;

  &__workarea {
    position: relative;
    flex: 1 0 60%;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  &__image-type {
    width: 90%;
    position: absolute;
    top: 30px; left: 30px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 20px;

    & div {
      cursor: pointer;
      flex: 1 0 auto;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 10px;
      background: var(--light);
      box-shadow: -4px -2px 16px #eaeaeb, 4px 2px 16px rgba(136, 165, 191, 0.48);

      &.active{
        background: var(--light);
      box-shadow: inset -3px -3px 7px #ffffff, inset 2px 2px 5px rgb(136 165 191 / 38%);

      }
    }

  }

  &__settings {
    margin-right: 16px;
    flex: 1 0 40%;
  }
}
.posttitle {
  font-size: 14px;
  margin-top: 8px;
}
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
    font-weight: 900;
    
    span {
      display: inline-block;
      width: 120px;
      position: absolute;
      transform: translate(-12.5px, 0px) rotate(var(--rot)) translate(0, -63px);
      text-align: center;
      height: 320px;
      top: -39px;
      text-shadow:0px 4px 3px rgb(255 255 255 / 42%), 0px 1px 6px rgb(255 255 255 / 75%);
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
#result {
  width: 300px;
  height: 300px;
  position: relative;
  top: 0; left: 0;
  margin-bottom: 20px;

  &.hide {
    display: none;
  }

}
.image-preview--result {
  display: block;
  left: 14%;
    top: 13%;
}
#resultcanvas {
  position: relative;
}
.canvaImg {
  /* position: absolute;
  border-radius: 50%; */
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
            getText: "",
            getSize: 12,
            myVal: null,
            showResult: null,
            previewImage: null,
            isHideResult: true,
            photo: "img/coin.png",
            width: 100,
            design: {
              gold: false,
              silver: true
            },
            type: {
              graving: true,
              colorPrint: false
            }
        }
        },
        components: {
          UploadImage
        },
        methods: {
           makeOrder() {
            this.isHideResult = !this.isHideResult
            setTimeout(() => {
               this.showResult = true;
            var canvas = document.querySelector('canvas');
            var svg = document.querySelector('#coin-svg');
            var xml = new XMLSerializer().serializeToString(svg);
            var svg64 = btoa(xml);
            var b64Start = 'data:image/svg+xml;base64,';
            var image64 = b64Start + svg64;

            // var img = document.querySelector('.result-image');
            
            // img.onload = function() {
              
              // draw the image onto the canvas
              // canvas.getContext('2d').drawImage(img, 0, 0);
            // }
            // img.src = image64;

            document.querySelector('.image-preview--result').innerHTML = `<img class="image-preview__image">`;
            var imgResult = document.querySelector('.image-preview__image');
            imgResult.src = image64;



            html2canvas(document.querySelector("#result")).then(function(canvas) {
              canvas.className = "test";
              let myscreen = canvas;
              var dataURL = canvas.toDataURL("image/png");
              document.getElementById("resultcanvas").appendChild(myscreen);

              // var newTab = window.open('about:blank','image from canvas');
              // newTab.document.write("<img src='" + dataURL + "' alt='from canvas'/>");
              let index = Math.floor(Math.random() * (1000 - 100 + 1) + 100);
              localStorage.setItem(`order-${index}`, JSON.stringify({photo: dataURL}));
            })
           
            }, 1000)


          },

        onFileSelected(event) {
            // console.log(event.target.files[0])
            let file = this.$refs.fileUploaded.files;
            if (file && file[0]) {
                let reader = new FileReader();
                reader.onload = (e) => {
                    this.previewImage = e.target.result;
                };
                reader.readAsDataURL(file[0]);
                // this.$emit('input', file[0])
            }
        },
        setGold() {
          this.photo = "img/coin2.png"
          this.design.silver = false
          this.design.gold = true
          $('.circle-wrapper p.circle').css({'color': 'rgb(100 75 3)'})
          $('#svg-filter-lighting').attr('lighting-color', '#ffd16c')
        },
        setSilver() {
          this.photo = "img/coin.png"
          this.design.silver = true
          this.design.gold = false
          $('.circle-wrapper p.circle').css({'color': 'rgb(0 0 0)'})
          $('#svg-filter-lighting').attr('lighting-color', '#fff')
        },
        modalClose() {
          this.isHideResult = true;
        },
        imageLeft() {
          let x = +$('#svgImage').attr('x')
          $('#svgImage').attr('x', x-2)
        },
        imageRight() {
          let x = +$('#svgImage').attr('x')
          $('#svgImage').attr('x', x+2)
        },
        imageTop() {
          let y = +$('#svgImage').attr('y')
          $('#svgImage').attr('y', y-2)
        },
        imageBottom() {
          let y = +$('#svgImage').attr('y')
          $('#svgImage').attr('y', y+2)
        },
        changeWidth(event) {
          $('#svgImage').attr('width', `${event.target.value}%`)
        },
        changeHeight(event) {
          $('#svgImage').attr('height', `${event.target.value}%`)
        },
        setGraving() {
          this.type.graving = true
          this.type.colorPrint = false
          $('#svgImage').attr('filter', 'url(#light)')
        },
        setColorPrint() {
          this.type.graving = false
          this.type.colorPrint = true
          $('#svgImage').attr('filter', '')

        },
        },
        computed: {
          myVal() {
            var circles = document.querySelectorAll('.circle')
            circles.forEach((circle) => {
              circle.innerHTML =
        this.getText
          .split("")
          .map((e, i) => {
            const fontSize = this.getSize;
            const start = Number(
              (-this.getText.length / 16) * 90
            );
            return `<span style="--rot:${
              start + i * 12
            }deg; font-size: ${fontSize}px">${e}</span>`;
          })
          .join("");
            })
          return this.getText;
          }
        },

    }
</script>
