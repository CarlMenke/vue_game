<template>
    <div class="relative">
        <div>
            <input placeholder="Height in px" name='height' v-on:input="(e)=>{setHeight(e)}"/>
            <input placeholder="Width in px" name='width' v-on:input="(e)=>{setWidth(e)}"/>
            <button @click="changeDimension">Apply</button>
        </div>
        <div class="game-container">
            <button class="button" v-if="!inGame" @click="startGame">Begin</button>
            <div v-if="inGame" class="timer">{{timer}}</div>
            <div v-if="inGame" class="lives"></div>
        </div>
    </div>
  </template>
  
  <script>

  export default {
    name: 'GameContainer',
    data: () =>{
      return {
        root: document.querySelector(':root'),
        height:400,
        width:400,
        timer:"0:0",
        timeBegan: null,
        started:null,
        inGame:false,
      }
    },
    props:{

    },
    mounted () {

    },
    methods: {
        changeDimension(){
            this.width > 199? this.root.style.setProperty(`--height-game`, `${this.height}px`):console.log("Minimum 200px")
            this.height > 199? this.root.style.setProperty(`--width-game`, `${this.width}px`):console.log("Minimum 200px")
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

            this.started = setInterval(this.clockRunning,10)
            this.inGame = true
        },
        clockRunning(){
            let currentTime = new Date()
            let timeElapsed = new Date(currentTime - this.timeBegan)
            let min = timeElapsed.getUTCMinutes()
            let sec = timeElapsed.getUTCSeconds()
            this.timer = `${min}:${sec}`
        },
        resetGame(){

        },
        stopGame(){

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
        top:5vh;
        margin:10px;
        border:2px solid grey;
        border-radius: 20px;
        background-color:rgb(220, 220, 220);
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
        border-radius: 5px;
        background-color: rgb(189, 189, 189);
        border:1px solid grey;
        padding:10px;
    }
    .button:hover{
        background-color: rgb(167, 167, 167);
        border:1px solid rgb(110, 110, 110);
    }
  </style>