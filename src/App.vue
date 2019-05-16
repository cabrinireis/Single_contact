<template>
  <div id="app">
    
    <formulario />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Formulario from './components/Form.vue'

export default {
  name: 'app',
  components: {
    Formulario
  }
}
</script>

<style>
.container{
margin-bottom: 10px;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}
body{
  
    background: url(./assets/back02.png)no-repeat center center;
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;
    background-position: top ;
  }
  
</style>
