<template>
    <h2>Choix des Joueurs</h2>
    <div class="Player1">
        <span>Joueur 1 :</span><br>
        <span name="Player1">Nom :</span>
        <input type="text" v-model="namePlayer1"><br>
        <span name="Symbol1">Choix du symbole :</span>
        <select v-model="symbolPlayer1">
            <option v-for="(symbol, indexPlayer1) of symbols" :key="indexPlayer1" @value="indexPlayer1">{{ symbol }}
            </option>
        </select>
    </div>
    <div class="Player2">
        <span>Joueur 2 :</span><br>
        <span name="Player2">Nom :</span>
        <input type="text" v-model="namePlayer2"><br>
        <span name="Symbol2">Choix du symbole :</span>
        <select v-model="symbolPlayer2">
            <option v-for="(symbol, indexPlayer2) of symbols" :key="indexPlayer2" @value="indexPlayer2">{{ symbol }}
            </option>
        </select>
    </div>
    <button @click="play">Jouer</button>

</template>
<script>
export default {
    name: 'InterfaceGame',
    data() {
        return {
            namePlayer1: '',
            symbolPlayer1: '',
            namePlayer2: '',
            symbolPlayer2: '',
            symbols: ['', 'X', 'O', '*', '-'],
            good: 'goodContent',
            bad: 'badContent'
        }
    },
    methods: {
        empty(content, update) {
            if (content != '') {
                update.classList.add(this.good);
                update.classList.remove(this.bad);
            } else {
                update.classList.add(this.bad);
                update.classList.remove(this.good);
            }
        },
        same(content1, content2, update1, update2) {
            if (content1 == content2) {
                update1.classList.remove(this.good);
                update2.classList.remove(this.good);
                update1.classList.add(this.bad);
                update2.classList.add(this.bad);
            }
        },
        play() {
            const Player1 = document.getElementsByName('Player1')[0];
            const Symbol1 = document.getElementsByName('Symbol1')[0];
            const Player2 = document.getElementsByName('Player2')[0];
            const Symbol2 = document.getElementsByName('Symbol2')[0];
            this.empty(this.namePlayer1, Player1);
            this.empty(this.symbolPlayer1, Symbol1);
            this.empty(this.namePlayer2, Player2);
            this.empty(this.symbolPlayer2, Symbol2);
            this.same(this.namePlayer1, this.namePlayer2, Player1, Player2);
            this.same(this.symbolPlayer1, this.symbolPlayer2, Symbol1, Symbol2);
            if (Player1.classList.contains(this.good) && Player2.classList.contains(this.good) && Symbol1.classList.contains(this.good) && Symbol2.classList.contains(this.good)) {
                this.$emit("PlayerList", [this.namePlayer1, this.namePlayer2]);
                this.$emit("SymbolList", [this.symbolPlayer1, this.symbolPlayer2]);
                this.nextstep();
            }
        },
        nextstep() {
            this.$emit('nextstep')
        }
    },
    props: {
        msg: String,
        symbolPlayers: []
    }
}
</script>
<style>
* {
    color: black;
}

span {
    padding: 5px;
    margin: 5px;
}

.badContent {
    color: red;
}

.goodContent {
    color: black;
}
</style>