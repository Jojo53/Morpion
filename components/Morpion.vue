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
    <button @click="reset">Recommencer</button>
</template>
<script>
export default {
    name: 'MorpionGame',
    data() {
        return {
            PlayerTurn: 0,
            Players: this.$parent.namePlayers,
            Symbols: this.$parent.symbolPlayers,
            sameLine: [],
            sameCol: [],
            sameDiagLeft: [],
            sameDiagRight: [],
        }
    },
    methods: {
        reset() {
            const tdList = document.getElementsByTagName('td');
            for (let index = 0; index < tdList.length; index++) {
                this.sameLine = [];
                this.sameCol = [];
                this.sameDiagLeft = [];
                this.sameDiagRight = [];
                tdList[index].innerHTML = '';
                this.PlayerTurn = 0;

            }
        },
        checkvalue(text) {
            for (let index = 0; index < this.Symbols.length; index++) {
                if (this.Symbols[index] == text.innerHTML) {
                    //console.log(this.Players[index] + ' gagne');
                    this.$parent.winner = this.Players[index];
                    this.nextstep();
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
            this.sameLine = [name];
            this.sameCol = [name];
            if (name.substring(0, 1) == name.substring(3, 2)) {
                this.sameDiagLeft = [name];
            }
            if (name == '1-3' || name == '2-2' || name == '3-1') {
                this.sameDiagRight = [name];

            }
            for (let index = 0; index < tdList.length; index++) {
                let td = tdList[index].getAttribute('name');

                if (td != name && tdList[index].innerHTML == text.innerHTML) {

                    //Lignes et Colonnes
                    if (td.substring(0, 1) == line) {
                        this.sameLine.push(td);
                        if (this.sameLine.length == 3) {
                            this.checkvalue(text);
                        }
                    }
                    if (td.substring(3, 2) == col) {
                        this.sameCol.push(td);
                        if (this.sameCol.length == 3) {
                            this.checkvalue(text);
                        }
                    }
                    //Diagonales
                    if (td.substring(0, 1) == td.substring(3, 2) && name.substring(0, 1) == name.substring(3, 2)) {
                        this.sameDiagLeft.push(td);
                        if (this.sameDiagLeft.length == 3) {
                            this.checkvalue(text);
                        }
                    }
                    if ((td == '1-3' || td == '2-2' || td == '3-1') && (name == '1-3' || name == '2-2' || name == '3-1')) {
                        this.sameDiagRight.push(td);
                        if (this.sameDiagRight.length == 3) {
                            this.checkvalue(text);
                        }
                    }
                }
            }
        },
        nextstep() {
            this.$parent.step++;
            this.$emit('nextstep');
        },
    }
}
</script>
<style>
:root {
    --border: 2px solid black;
}


table {
    margin: 0 auto;
    width: 50%;
    height: 50%;
    padding: 0.5em;
    border: var(--border);
    border-radius: 1em;
    border-spacing: 0;
}

td {
    width: 10vw;
    height: 10vh;
    font-size: 5em;
}

td[name="1-1"],
td[name="1-3"],
td[name="3-1"],
td[name="3-3"] {
    border: var(--border);
}

td[name="1-1"] {
    border-top-left-radius: 0.25em;
}

td[name="1-2"],
td[name="3-2"] {
    border-top: var(--border);
    border-bottom: var(--border);
}

td[name="2-1"],
td[name="2-3"] {
    border-left: var(--border);
    border-right: var(--border);
}

td[name="1-3"] {
    border-top-right-radius: 0.25em;
}

td[name="3-1"] {
    border-bottom-left-radius: 0.25em;
}

td[name="3-3"] {
    border-bottom-right-radius: 0.25em;
}

td:hover {
    cursor: pointer;
    background-color: red;
}

@media screen and (max-width: 600px) {
    td {
        font-size: 2em;
    }
}
</style>