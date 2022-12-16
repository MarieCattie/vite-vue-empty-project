<template lang="">
        
        <div :class="{'visible': this.previewImage}" class="image-preview" @click="selectImage">
            <svg id="coin-svg" viewBox="0 0 300 300" width="220px" 
                        xmlns="http://www.w3.org/2000/svg"
                        xmlns:xlink="http://www.w3.org/1999/xlink">
                    <filter id="light">
                        <!-- VARIANT1 -->
                        <!-- blur the source image to make bump map less sharp -->
                        <!-- <feGaussianBlur stdDeviation="7" result="blurred"></feGaussianBlur> -->
                        <!-- create bump map based on alpha channel -->
                        <!-- <feColorMatrix in="blurred" type="luminanceToAlpha" result="bumpMap"></feColorMatrix> -->
                        <!-- use bump map for lighting filter -->
                        <!-- <feDiffuseLighting in="bumpMap" surfaceScale="8" result="light">
                        <fePointLight x="225" y="150" z="120"></fePointLight>
                        </feDiffuseLighting> -->
                        <!-- compose the lighting result with source image using multiplication -->
                        <!-- <feComposite in="light" in2="SourceGraphic"
                        operator="arithmetic"
                        k1="1" k2="0" k3="0" k4="0" result="bump">
                        </feComposite>
                        <feColorMatrix type="saturate" values="0" x="0%" y="0%" width="100%" height="100%" in="bump" result="colormatrix"/> -->

                        <!-- VARIANT2-->
                        <feColorMatrix type="luminanceToAlpha" />
                        <!-- <feDiffuseLighting diffuseConstant="1" surfaceScale="1" result="diffuse3">
                        <fePointLight x="50" y="25" z="15"/> 
                        <feDistantLight elevation="30" azimuth="200" /></feDiffuseLighting>   -->

                        <feDiffuseLighting id="svg-filter-lighting" diffuseConstant="1" surfaceScale="1.5" result="diffuse3" lighting-color="#fff" in="colormatrix">
                            <fePointLight x="150" y="125" z="85"></fePointLight>
                            <feDistantLight elevation="30" azimuth="200"></feDistantLight>
                        </feDiffuseLighting>
                    </filter>
                     <image id="svgImage"  filter="url(#light)" v-bind:href="previewImage" width="100%" x="0" y="0"></image>
            </svg>

        </div>
</template>

<script>
import { ref } from "vue";
export default {
    data() {
        return {
            
        };
    },
    props: ['previewImage', 'width'],

    methods: {
        selectImage() {
            this.$refs.fileUploaded.click();
        },
    },
    watch: {},
};
</script>

<style lang="scss">
#coin {
    display: inline-block;
    position: relative;
}
.image-preview {
    display: none;
    width: 220px;
    height: 220px;
    left: 14%;
    top: 13%;
  /*  transform: translate(-50%, -46%);*/
    transform-origin: center;
    overflow: hidden;
    position: absolute;
    z-index: 1000;
    border-radius: 50%;

    &.visible {
        display: block;
    }

    & img {
        width: 220px;
        height: 220px;
        object-fit: cover;
        

        &.filtered {
            filter: url(#light);
        }
    }
}
</style>