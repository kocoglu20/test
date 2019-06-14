<template>
    <div>
        <p class="counter-container text-center"> Sayaç : {{ double }}</p>
        <p class="counter-container text-center"> {{ stringC }}</p>
        <input type="text" v-model="value" class="form-control">
        <p>{{ value }} {{ pozisyon }}</p>
    </div>
</template>
<script>
    import { mapGetters } from "vuex";
    export default {
        //props : ["counter"]
        /*
        computed:{
            counter(){
                //return this.$store.state.counter;
                return this.$store.getters.getDoubleCounter;
            },
            stringCounter(){
                return this.$store.getters.stringCounter;
            }
        }
         */
        computed : {
            ...mapGetters({
                double: 'getDoubleCounter',
                stringC: 'stringCounter',
                pozisyon: 'getPozisyon'
            }),
            value:{
                get(){
                    return this.$store.getters.getValue;
                },
                set(value){
                    this.$store.dispatch("setValueData", value);
                }
            }
        },
        methods:{
            /*
            setValue(event) {
                this.$store.dispatch("setValueData", event.target.value)
            }
             */
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