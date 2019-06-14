<template>
    <div>
        <button class="btn btn-success" @click="increaseCounter(1)">+ Arttır</button>
        <button class="btn btn-danger" @click="decreaseCounter">- Azalt</button>
        <hr>
        <button class="btn btn-success" @click="increment(1)">+ Arttır</button>
        <button class="btn btn-danger" @click="decrement">- Azalt</button>
        <hr>
        <button class="btn btn-success" @click="incAsync({time:1000, veri:1})">+ Async Arttır</button>
    </div>
</template>

<script>
    import { mapMutations, mapActions } from "vuex";
    export default {
        methods : {
            /*
            incrementCounter(){
                //this.$emit("counterEvent", 1);
                //this.$store.state.counter++;
                //this.$store.commit("updateCounter",1);
                this.$store.commit("increaseCounter");
            },
            decrementCounter(){
                //this.$emit("counterEvent", -1);
                //this.$store.state.counter--;
                //this.$store.commit("updateCounter",-1);
                this.$store.commit("decreaseCounter");
            }
             */
            ...mapMutations([
                'increaseCounter',
                'decreaseCounter'
            ]),
            ...mapActions([
                "increment",
                "decrement",
                "incAsync"
            ])
            /*
            increment(){
                this.$store.dispatch("increment");
            },
            decrement(){
                this.$store.dispatch("decrement");
            },
            incrementAsync(){
                this.$store.dispatch("incAsync");
            }
             */
        }
    }
</script>

<style>
</style>