<template>
    <table>
        <tr>
            <td name="1-1" @click="choice($event)"></td>
            <td name="1-2" @click="choice($event)"></td>
            <td name="1-3" @click="choice($event)"></td>
        </tr>
        <tr>
            <td name="2-1" @click="choice($event)"></td>
            <td name="2-2" @click="choice($event)"></td>
            <td name="2-3" @click="choice($event)"></td>
        </tr>
        <tr>
            <td name="3-1" @click="choice($event)"></td>
            <td name="3-2" @click="choice($event)"></td>
            <td name="3-3" @click="choice($event)"></td>
        </tr>
    </table>
</template>
<script>
export default {
    name: 'MorpionGame',
    data() {
        return {
            PlayerTurn: 0,
            Players: this.$parent.namePlayers,
            Symbols: this.$parent.symbolPlayers,
            same: [],
        }
    },
    props: {

    },
    methods: {
        checkvalue(text) {
            if (this.same.length == 3) {
                for (let index = 0; index < this.Symbols.length; index++) {
                    if (this.Symbols[index] == text.innerHTML) {
                        console.log(this.Players[index] + ' gagne');
                    }
                }
            }
        },
        choice(event) {
            let name = event.target.getAttribute('name');
            const text = document.getElementsByName(name)[0];
            if (this.PlayerTurn == this.Players.length) {
                this.PlayerTurn = 0;
            }
            for (let index = this.PlayerTurn; index < this.Players.length; index++) {
                if (this.PlayerTurn == index) {
                    if (text.innerHTML == '') {
                        text.innerHTML = this.Symbols[index];
                        this.PlayerTurn++;
                    }
                }
            }
            //Recupération de la ligne
            const line = name.substring(0, 1);
            //Recupération de la colonne
            const col = name.substring(3, 2);
            //Liste des Elements
            const tdList = document.getElementsByTagName('td');
            this.same = [name];
            for (let index = 0; index < tdList.length; index++) {
                let td = tdList[index].getAttribute('name');
                if (td != name && tdList[index].innerHTML == text.innerHTML) {
                    //Lignes et Colonnes
                    if (td.substring(0, 1) == line || td.substring(3, 2) == col) {
                        this.same.push(td);
                        this.checkvalue(text);
                    }
                    //Diagonales
                    if (td.substring(0, 1) == td.substring(3, 2)) {
                        this.same.push(td);
                        this.checkvalue(text);
                    }
                }
            }
        }
    }
}
</script>
<style>
table {
    margin: 0 auto;
    border: 1px solid black;
    width: 50%;
    height: 50%;
}

td {
    width: 20px;
    height: 20px;
    border: 1px solid black;
}

td:hover {
    cursor: pointer;
}
</style>