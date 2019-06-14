<template>
    <div class="alan" v-draggable="draggableValue">
        <slot/>
        <b-button class="btn-block mb-1" v-b-popover="{title:left + '-' + top, content:left + '-' + top}">{{pozisyon}}</b-button>
    </div>
</template>

<script>
    import { Draggable } from 'draggable-vue-directive'

    export default {
        props:["alanNo","arttir","azalt"],
        directives: {
            Draggable,
        },
        data() {
            return {
                draggableValue: {
                    onPositionChange: this.onPosChanged
                },
                left:0,
                top:0
            };
        },
        computed:{
            pozisyon(){
                return this.left + '|' + this.top;
            }
        },
        methods: {
            increaseCounter(){
                this.$emit("data", {alanNo: this.alanNo, left: this.left,top: this.top});
            },
            onPosChanged: function(positionDiff, absolutePosition, event) {
                this.left = absolutePosition.left;
                this.top = absolutePosition.top;
                this.$emit("data", {alanNo: this.alanNo, left: this.left,top: this.top});
            }
        }
    }

</script>
<style scoped>
    div.alan {
        background: blue;
        color: white;
        text-align: center;
        width: 100px;
        height: 60px;
    }
</style>