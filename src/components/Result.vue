<template>
    <div>
        <p class="counter-container text-center">{{ pozisyon }} Sayaç : {{ counter }}</p>
    </div>
</template>
<script>
    export default {
        //props : ["counter"]
        computed:{
            counter(){
                //return this.$store.state.counter;
                return this.$store.getters.getDoubleCounter;
            },
            pozisyon(){
                return this.$store.state.pozisyon;
            }
        }
    }

</script>
<style scoped>
    .counter-container{
        border: 1px solid #aa7f08;
        padding: 3px 5px;
        background-color: #fbbd08;
        font-size: 20px;
        color: #000;
    }
</style>