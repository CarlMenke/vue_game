<template>
  <div id="app">
    <WelcomePage  @beginGame="beginGame"/>
    <GameContainer :inGame="inGame"/>
  </div>
</template>

<script>
import WelcomePage from './components/WelcomePage.vue'
import GameContainer from './components/GameContainer.vue'

export default {
  name: 'App',
  components: {
    WelcomePage,
    GameContainer
  },
  data: () =>{
    return {
      inGame:false
    }
  },
  methods: {
    beginGame(){
      this.inGame = true;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
