<template>
  <div >
    <div class="title">
      <h1> Aim Helper </h1>
      <img alt="Vue logo" src="../assets/target.png">
    </div>
    <h3>Rules:</h3>
    <ul>
      <li>1. When a circle appears, click it as fast as you can.</li>
      <li>2. You will have a certain amount of time to click it before it disappears.</li>
      <li>3. If a circle disappears with out you clicking it, you lose a life.</li>
      <li>4. You have 3 lives, how long can you last?</li>
    </ul>
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
    
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
li{
  list-style: none;
}
.title{
  display:flex;
  flex-flow:row nowrap;
  justify-content: center;
  align-items: center;
}
</style>
