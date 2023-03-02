<template>
    <div class="wrapper clearfix">
        <comp-player :scorePlayer="scorePlayer" :activePlayer="activePlayer" :currentScore="currentScore" />
        <comp-control @handleNewGame="handleNewGame" @handleRollDices="handleRollDices" @handleHoldScore="handleHoldScore"
            @handleFinalScore="handleFinalScore" :isPlaying="isPlaying" />
        <comp-dice :dices="dices" />
        <comp-rule :isOpenPopup="isOpenPopup" @handleOffPopup="handleOffPopup" />
    </div>
</template>

<script>
import compControl from './components/compControl.vue'
import compPlayer from './components/compPlayer.vue'
import compDice from './components/compDice.vue'
import compRule from './components/compRule.vue'
export default {
    name: 'App',
    components: {
        compDice,
        compPlayer,
        compControl,
        compRule
    },
    data() {
        return {
            scorePlayer: [1, 4],
            currentScore: 10,
            activePlayer: 1,
            isPlaying: false,
            isOpenPopup: false,
            dices: [1, 3],
            finalScore: 0
        }
    },
    methods: {
        handleFinalScore(finalScoreControl) {
            this.finalScore = finalScoreControl
        },
        nextPlayer() {
            this.currentScore = 0
            if (this.activePlayer == 1) {
                alert(`Player ${this.activePlayer + 1} đã quay vào xúc xắc 1! Lượt chơi chuyển sang player ${this.activePlayer}`)
                this.activePlayer = 0
            } else {
                alert(`Player ${this.activePlayer + 1} đã quay vào xúc xắc 1! Lượt chơi chuyển sang player ${this.activePlayer + 2}`)
                this.activePlayer = 1
            }
        },
        handleNewGame() {
            this.isOpenPopup = true
        },
        handleHoldScore() {
            if (this.activePlayer == 1) {
                this.activePlayer = 0
                this.scorePlayer[1] += this.currentScore
            } else {
                this.activePlayer = 1
                this.scorePlayer[0] += this.currentScore
            }
            this.currentScore = 0
            if (this.scorePlayer[0] >= this.finalScore) {
                alert("Player 1 đã chiến thắng")
                this.isPlaying = false
            }
            if (this.scorePlayer[1] >= this.finalScore) {
                alert("Player 2 đã chiến thắng")
                this.isPlaying = false
            }
        },
        handleOffPopup() {
            this.isOpenPopup = false
            this.isPlaying = true
            this.currentScore = 0
            this.activePlayer = 0
            this.scorePlayer = [0, 0]
            this.dices = [1, 1]
        },
        handleRollDices() {
            if (this.isPlaying == true) {
                let dice1 = Math.floor(Math.random() * 6 + 1)
                let dice2 = Math.floor(Math.random() * 6 + 1)
                this.dices = [dice1, dice2]
                if (dice1 == 1 || dice2 == 1) {
                    this.nextPlayer()
                } else {
                    this.currentScore += dice1 + dice2
                }
            } else {
                alert("Bạn phải tạo game mới!")
            }
        }
    }
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.clearfix::after {
    content: "";
    display: table;
    clear: both;
}

body {
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url(./assets/back.jpg);
    background-size: cover;
    background-position: center;
    font-family: Lato;
    font-weight: 300;
    position: relative;
    height: 100vh;
    color: #555;
}

.wrapper {
    width: 1000px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
    overflow: hidden;
}
</style>