<template>
  <div class="Weather">
    
    <img v-if="img === 1 " height="100vh" width="100vw" src="./assets/deszcz.jpg">
    <img v-if="img === 2" height="100vh" width="100vw" src="./assets/sun.jpg">
    <img v-if="img === 3" height="100vh" width="100vw" src="./assets/snow.png">
    <img v-if="img === 4" height="100vh" width="100vw" src="./assets/clouds.jpg">
  </div>
</template>

<script>
export default {
  name: 'ChosenWeather', 
   props: ["img"],
   

}
</script>

<style scoped>

h2 {
  color: #42b983;
  font-size: 50px;
  background-color: hotpink;
  opacity: .66;
}
</style>