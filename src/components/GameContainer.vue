<template>
    <div class="relative">
        <div class="info-box">
            <div class="info-top">
                <div class="prefix">Your Lives:</div>
                <div class="suffix">{{lives}}</div>
            </div> 
            <div class="info-top">
                <div class="prefix">Score:</div>
                <div class="suffix">{{playerScore}}</div>
            </div>
        </div>
        <div >
            <input class="button" placeholder="Height in px" name='height' v-on:input="(e)=>{setHeight(e)}"/>
            <input class="button" placeholder="Width in px" name='width' v-on:input="(e)=>{setWidth(e)}"/>
            <button class="button" @click="changeDimension">Apply</button>
        </div>
        <div class="game-container">
            <div class="game" >
                <ClickCircle class="circle" v-for="circle in circleArray" :key="circle.id"  :circle="circle" @handleCircleClick="handleCircleClick" @handleLooseLife="handleLooseLife"/>
            </div>
            <button class="button" v-if="!inGame" @click="startGame">Begin</button>
            <div v-if="!inGame" class="info-top">
                <div class="prefix">Score:</div>
                <div class="suffix">{{playerScore}}</div>
            </div>
            <div v-if="inGame" class="timer">{{timer}}</div>
            <div v-if="inGame" class="lives"></div>
        </div>
    </div>
  </template>
  
  <script>
  import ClickCircle from './ClickCircle.vue'
  export default {
    name: 'GameContainer',
    components:{
        ClickCircle
    },
    data: () =>{
      return {
        root: document.querySelector(':root'),
        height:400,
        width:400,
        timer:"0",
        timeBegan: null,
        started:null,
        inGame:false,
        circleArray:[],
        lives:3,
        circleId:0,
        playerScore:0
      }
    },
    props:{
    },
    mounted () {
    },
    methods: {
        changeDimension(){
            this.width > 199? this.root.style.setProperty(`--height-game`, `${this.height}px`):this.root.style.setProperty(`--height-game`, `200px`)
            this.height > 199? this.root.style.setProperty(`--width-game`, `${this.width}px`):this.root.style.setProperty(`--width-game`, `200px`)
        },
        setHeight(e){
            this.height = e.target.value
        },
        setWidth(e){
            this.width = e.target.value
        },
        startGame() {
            if(this.inGame){return}

            if(!this.timeBegan){
                this.timeBegan = new Date()
            }

            this.lives=3
            this.playerScore=0
            this.started = setInterval(this.clockRunning,10)
            this.inGame = true

            const pause = () =>{
                return new Promise((resolve)=>{
                    console.log('timer', this.timer)
                    setTimeout(resolve, this.circleId < 15 ? 850: this.circleId < 30 ? 750: this.circleId < 45? 650 : this.circleId < 60 ? 550 : this.circleId < 75 ? 500 : 450)
                })
            }
            const createCircle = () =>{
                if(this.inGame){
                    const circle = {
                    height:15+Math.random()*70,
                    width: 15+Math.random()*70,
                    id:this.circleId,
                    clicked:false
                }
                this.circleId++
                console.log(circle)
                return circle
                }
            }
            const continueGame = async () =>{
                if(this.inGame){
                    const newCircle =  createCircle()
                    this.circleArray.push(newCircle)
                    await pause()
                    continueGame()
                }
            }

            continueGame()
        },
        clockRunning(){
            let currentTime = new Date()
            let timeElapsed = new Date(currentTime - this.timeBegan)
            let min = timeElapsed.getUTCMinutes()
            let sec = timeElapsed.getUTCSeconds()
            this.timer = min>0?`${min}:${sec}`:`${sec}`
        },
        resetGame(){

        },
        stopGame(){

        },
        handleCircleClick(id){
            this.playerScore++
            document.getElementById(id).remove()
        },
        handleLooseLife(id){
            this.lives--
            if(this.lives === 0){
                this.inGame = false
                for(let i = 0; i < this.circleArray.length; i++){
                    document.getElementById(i)?document.getElementById(i).remove():null
                }
            this.timer="0"
            this.timeBegan=null
            this.started=null
            this.inGame=false
            this.circleArray=[]
            this.circleId=0
            }
            document.getElementById(id)?document.getElementById(id).remove():null
            console.log(this.lives)
        }
    }
  }
  </script>
  
  <style >
    :root {
        --width-game:400px;
        --height-game:400px;
    }
    .game-container{
        position:absolute;
        display:flex;
        flex-flow: row nowrap;
        justify-content: center;
        align-items: center;
        top:15vh;
        margin:10px;
        border: 2px solid #3c8871;
        border-radius: 20px;
        background-color: #dbe8e4;
        width:var(--width-game);
        height:var(--height-game)
    }
    .relative{
        top: 3vh;
        position:relative;
        display:flex;
        flex-flow:column nowrap;
        justify-content: center;
        align-items: center;
        margin:10px;
    }
    .timer{
        font-family:Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
        opacity: .13;
        font-size: 5em;
    }
    .button{
        z-index:2;
        border-radius: 5px;
        background-color: rgb(189, 189, 189);
        border:1px solid grey;
        padding:10px;
    }
    .button:hover{
        background-color: rgb(167, 167, 167);
        border:1px solid rgb(110, 110, 110);
    }
    .game{
        position:absolute;
        width:100%;
        height:100%;
        border-radius:10px;
    }
    .circle{
        z-index:4;
    }
    .info-top{
        display:flex;
        flex-flow:row nowrap;
        align-items: center;
        justify-content: center;
        border-radius:5px;
        border: 2px solid #3c8871;
        padding:10px;
        background-color: #e3efeb;
        margin:5px; 
    }
    .info-box{
        display: flex;
        flex-flow: row nowrap;
    }
    .button{
        border-radius:5px;
        border: 2px solid #3c8871;
        padding:10px;
        background-color: #e3efeb;
        margin:2px;
        width:20%;
    }
    .button:hover{
        border: 2px solid #539c86;
        background-color: #c0dcd2;
    }
    .prefix{
        display:inline;
        margin:2px
    }
    .suffix{
        display:inline;
        font-size: 1.5em;
        font-weight: bold;
        margin:3px;
    }
  </style>