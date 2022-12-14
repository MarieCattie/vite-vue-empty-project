<template lang="">
        <div v-if="!hidden" class="popup">
            <div class="popup__inner">
                <p class="popup__text">{{popup}}</p>
                <button @click="close">
                    <span class="material-icons material-symbols-outlined">
                        close
                    </span>    
                
                </button>
            </div>
        </div>
</template>

<script>
    import {ref} from 'vue'
    export default {
        data() {
        return {
            hidden: true,
            popup: null
        }
        },

        methods: {
            close() {
                this.hidden = true
            },
            change() {
                this.popup = document.querySelector('#textPopup').value
            }
        },
        watch: {
            popup() {

            },
            hidden(val) {
                if(val) {
                    this.popup = null
                }
            }
        }
    }


    // const popup = ref(null)

    // const popupText = computed({
    //     get() {
    //         return popup.value
    //     },
    //     set(val) {
    //         popup.value = val
    //     }
    // })
</script>

<style lang="scss" scoped>
    .popup {
        z-index: 100000;
        display: block;
        position: fixed;
        bottom: 30px;
        right: 30px;

        &__inner {
            background-color: var(--primary);
            border-radius: 30px;
            padding-top: 10px;
            padding-bottom: 10px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding-left: 60px;
            padding-right: 60px;
        }

        &__text {
            text-align: center;
        }
        
    }
</style>