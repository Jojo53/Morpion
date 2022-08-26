<template>
    <h2>Les Règles du Jeu</h2>
    <div>
        <ul>
            <li>Chaque joueur est représenter par un symbole.</li>
            <li>Un joueur utilise toujours le même symbole.</li>
            <li>Un premier joueur desssine son symbole sur une case.
                Puis c'est au tour de l'autre joueur de dessiner son symbole sur une case vide.</li>
            <li>Le but du jeu est de réussir à aligner ses trois symboles(horizontal, vertical ou diagonale).</li>
        </ul>
    </div>
    <input type="button" value="Choix des Joueurs" @click="nextstep">
</template>
<script>
export default {
    name: 'RulesGame',
    props: {
        msg: String
    },
    methods: {
        nextstep() {
            this.$emit('nextstep')
        }
    }
}
</script>
<style>
ul {
    list-style-type: none;
}
</style>