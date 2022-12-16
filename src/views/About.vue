<template lang="">
    <main class="about-page">
        <h1>Корзина</h1>
        
        <p>Здесь вы можете просмотреть свои заказы</p>
        <div class="orders">
            
        </div>
    </main>
</template>
<script>
export default {
    data() {
        return {
        }
        },
        components: {
          
        },
        methods: {
          makeOrder() {
          }
        },
        mounted() {
         
            for(var x in localStorage){
                if(x.indexOf("order-")==0){
                    let order = JSON.parse(localStorage.getItem(x));
                    let div = 
                    `
                    <div class='order'>
                        <div class='order__image'>
                            <img src=${order.photo}>
                        </div>
                        <div class='order__content'>
                            <h3>Тип: ${order.type}</h3>
                            <h6>Материал: ${order.material}</h6>
                            <p>Текст на медали: ${order.text}</p>
                            <p>Размер шрифта: ${order.size}</p>
                        </div>
                        
                    </div>
                    `
                    $('.orders').append(div)
                }

}
          
        },
}
</script>
<style lang="scss">
    .order {
        display: flex;
        align-items: center;
        margin-top: 30px;
        margin-bottom: 30px;
        &__image {
            width: 230px;
            height: 230px;
            border-radius: 50%;
            overflow: hidden;
            & img {
                width: 100%;
                height: 100%;
                object-fit: contain;
            }
        }
        &__content {
            margin-left: 20px;
            & * {
                margin-bottom: 10px;
            }
        }
    }
    
</style>