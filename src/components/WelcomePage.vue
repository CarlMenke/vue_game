<template>
  <div >
    <img alt="Vue logo" src="../assets/logo.png">
    <h1> Welcome To Quick Click </h1>
    <h3>Rules:</h3>
    <ul>
      <li>1. When a circle appears, click it as fast as you can.</li>
      <li>2. You will have a certain amount of tim eto click it before it disappears.</li>
      <li>3. If a circle disappearts with out you clicking it, you lose a life.</li>
      <li>4. You have 3 lives, how long can you last?</li>
    </ul>
    <button @click="beginGame">Begin</button>
  </div>
</template>

<script>
export default {
  name: 'WelcomePage',
  data: () =>{
    return {

    }
  },
  methods: {
    beginGame(){
      this.$emit(
        "beginGame"
      )
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
li{
  list-style: none;
}
</style>
