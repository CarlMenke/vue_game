<template>
  <div id="app">
    <WelcomePage />
    <GameContainer />
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

    }
  },
  methods: {

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #3c8871;
  margin-top: 60px;
}
</style>
