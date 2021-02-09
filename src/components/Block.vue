<template>
    <div class="block" v-if="showBlock" @click="stopTimer">
        Click me
    </div>
</template>
<script>
export default {
    props: ['delay'],

    data(){
        return {
            showBlock: false,
            timer: null,
            reactionTime: 0,
        }
    },

    // po apacia yra du hooks kurie naudojami tam tikrai data, tai galima pasiziureti Lifecycle Hooks diagramoje vue.js
    mounted() {
        console.log('component mounted');
        setTimeout(() => {
            this.showBlock = true;
            console.log(this.delay);
            this.startTimer()
        }, this.delay)
    },

    // updated() {
    //     console.log('component updated');
    // },

    // unmounted() {
    //     console.log('unmounted');
    // },

    methods: {
        startTimer() {
            // tipo funkcija funkcijoje, nes nurodome setInterval viduje funkcija
            this.timer = setInterval(() => {this.reactionTime += 10}, 10)
        },

        stopTimer() {
            // tai logika tokia kad kai paspaudi play tada tarp 2-7s paleidzia green block, tada kai ju ti 
            // paspaudi iskviecia settimer funkcija ir iraso tavo rezultata pridedamas 10ms, bei kai paspaudi green block
            // tada isvalo intervala ir timer kintamaji. ir taip iraso reakcijos laika i reactiontimer kintamaji ir
            // nunulina intervala paspaudus green block.
            clearInterval(this.timer)
            console.log(this.reactionTime);
            // su $emit perduoda data i App.vue faila
            this.$emit('end', this.reactionTime)
        }
    }
}
</script>

<style>
    .block {
        width: 400px;
        background: #0faf87;
        border-radius: 20px;
        color: white;
        text-align: center;
        padding: 100px 0;
        margin: 40px auto;
    }
</style>