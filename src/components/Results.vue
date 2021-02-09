// emmiting custom
<template>
<div>
    <p>Reaction time - {{ score }} ms</p>
    <!-- butinai reikia tevinio elemento div -->
    <p class="rank">{{ rank }}</p>
</div>
</template>

<script>
export default {
    // props yra masyvas ne objektas tai jam reikia lauztiniu skliaustu
    props: ['score'],
    data () {
        return {
            rank: null,
        }
    },
    mounted() {
        if (this.score < 250) {
            this.rank = 'Ninja Fingers';
        }   else if (this.score < 400) {
            this.rank = 'Rapid Reflexes'
        }   else {
            this.rank = 'Snail pace...'
        }
    }
}
</script>

<style>
    .rank {
        font-size: 1.4em;
        color: #0faf87;
        font-weight: 700;
    }
</style>