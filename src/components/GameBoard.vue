<script setup>
import {ref, computed} from 'vue'

const winner = ref('')

const isActive = ref(false);

const gameEnded = ref(false);

const resetGameboard = () => {gameboard.value = [
    ['','',''],
    ['','',''],
    ['','','']
]
gameEnded.value = false
isActive.value = false
winner.value = ""
}

const gameboard = ref([
    ['','',''],
    ['','',''],
    ['','','']
])
const winningCondition = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]]

const calcWinner = () => {
    let board = gameboard.value.flat()
    for (let i= 0; i < winningCondition.length; i++){
        let cellone = winningCondition[i][0]
        let celltwo = winningCondition[i][1]
        let cellthree = winningCondition[i][2]
        
        
        // same with decontruction
        // const [a, b, c] = winningCondition[i]

        if (board[cellone] && board[cellone] === board[celltwo] && board[cellone] === board[cellthree]){
            console.log('yes yes yo')
            return `The winner is player: ${board[cellone]}`
        }
    }
}
const calcTie = () => {
    let board = gameboard.value.flat()
    for (let i=0;i<board.length;i++){
       
        if (board[i] === ""){
            //console.log('Still Going')
            return
        }
        

    }
    return ('The Game is a tie')
}

const playerturn = ref('X')

const playMove = (rowi,columni) => {  
    
    if (gameEnded.value === true) {
        return
    }

    if (gameboard.value[rowi][columni]){
        return
    }
    
    gameboard.value[rowi][columni] = playerturn.value
    playerturn.value = playerturn.value === 'X' ? 'O' : 'X'
    const calctie = calcTie()
    if (calctie) {
        winner.value = calctie
        isActive.value = true
        gameEnded.value = true
    }
    const calcwinner = calcWinner()
    if (calcwinner) {
        winner.value = calcwinner
        isActive.value = true
        gameEnded.value = true
    } 
    
    
}
</script>

<template>
    <div class="board">
        <div v-for="(row,rowi) in gameboard" key:="rowi" class="rows">
            <div v-for="(cell,columni) in row" key:="columni" class="cells">
                <button @click="playMove(rowi,columni)" class="cell ":id="`cell${rowi}${columni}`">{{ cell }}</button>             
            </div>

        </div>
    </div>
    <div class="winning"> <h1>{{ winner }}</h1></div>
    <div class="reset">
        <button @click="resetGameboard()" class="resetButton" :class="{showButton: isActive}">RESET</button>
    </div>
</template>

<style>
    .board{
    display: grid;
    width: 300px;  
    height: 300px;
    grid-template-columns: auto auto auto;
    }
    .cell {
        display: flex;
        width: 100px;
        height: 100px;
        align-items: center;
        justify-content: center;
        font-size: 3rem;
        font-weight: bold;
        border: 3px solid black;
        transition: background 0.2s ease-in-out;
    }
    button:hover{
        cursor: pointer;
    }
    .resetButton{
        display: none;
    }
    .showButton{
        display: flex;
        border: 3px solid black;
        font-size: 2rem;
    }
    .winning {
        color: orange;
        /* text-shadow: 2px 2px 2px black; */
    }
    
</style>