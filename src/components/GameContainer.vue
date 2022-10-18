<template>
    <div class="relative">
        <div>
            <input placeholder="Height in px" name='height' v-on:input="(e)=>{setHeight(e)}"/>
            <input placeholder="Width in px" name='width' v-on:input="(e)=>{setWidth(e)}"/>
            <button @click="changeDimension">Apply</button>
        </div>
        <div class="game-container">
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
        width:400
      }
    },
    props:{
        inGame: Boolean
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
  </style>