<template>
    <div v-if="!clicked" :id="this.circle.id" class="circle-container" @click="(e)=>{handleCircleClick(e)}">
        <img  :id="this.circle.id" :src="target"/>
    </div>
  </template>
  
  <script>
  import target from '../assets/target.png'
  export default {
    name: 'ClickCircle',
    data: () =>{
      return {
        target:target,
        clicked:false
      }
    },
    props:{
        circle:Object
    },
    mounted () {
        const root = document.getElementById(`${this.circle.id}`)
        root.style.setProperty(`--height`, `${this.circle.height}%`)
        root.style.setProperty(`--width`, `${this.circle.width}%`)
        setTimeout(()=>{
            console.log(document.getElementById(`${this.circle.id}`))
            document.getElementById(`${this.circle.id}`)?this.handleLooseLife():null
        },2500)
    },
    methods: {
       handleCircleClick(e){
        this.$emit('handleCircleClick', e.target.attributes.id.value)
       },
       handleLooseLife(){
        this.$emit('handleLooseLife', this.circle.id)
       }
    }
  }
  
  </script>
  
  <style scoped>
    :root {
        --width:0%;
        --height:0%;
    }
    .circle-container{
        position:absolute;
        bottom:var(--height);
        left:var(--width);
        animation-name: target;
        animation-duration: 3s;
        z-index:3;
    }
    @keyframes target {
        0% {scale:0;}
        50% {scale:1;}
        100% {scale:0;}
    }
  </style>