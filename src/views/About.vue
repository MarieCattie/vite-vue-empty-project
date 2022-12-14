<template lang="">
    <main class="about-page">
        <h1>About</h1>
        
        <p>This is about page</p>
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
                    <div>
                        <img src=${order.photo}>
                    </div>
                    `
                    $('.orders').append(div)
                }

}
          
        },
}
</script>
<style lang="">
    
</style>