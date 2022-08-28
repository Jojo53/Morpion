<template>
    <div>
        <span>{{ winner }} à gagné</span><br>
        <img class="victory" src="../assets/victory.gif" alt="Victoire"><br>
        <button @click="reset">Recommencer</button>
    </div>
</template>
<script>
export default {
    name: 'WinGame',
    data() {
        return {
            winner: this.$parent.winner,
            step: this.$parent.step,
        }
    },
    methods: {
        reset() {
            this.$parent.step = 3;
            this.$emit('nextstep');
        }
    },
    props: {
        msg: String,

    }
}
</script>
<style>
.victory {
    width: 20vw;
    margin-top: 5px;
}

@media screen and (max-width: 600px) {
    .victory {
        width: 30vw;
    }
}
</style>