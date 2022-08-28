<template>
    <h1>{{ msg }}</h1>
    <img src="../assets/tic-tac-toe.png" alt="Tic Tac Toe">
</template>
<script>
export default {
    name: 'MainGame',
    props: {
        msg: String
    },
}
</script>
<style>
img {
    width: 15vw;
}

@media screen and (max-width: 600px) {
    img {
        width: 20vw;
    }
}
</style>