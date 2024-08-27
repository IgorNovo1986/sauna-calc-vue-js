<template>
  <div class="container">
    <div class="logo">
      <img
          alt="sauna"
          src="./assets/logo.png"
      >
    </div>
    <SaunaCalculation />
  </div>
</template>

<script>
import SaunaCalculation from './components/SaunaCalculation.vue'

export default {
  name: 'App',
  components: {
    SaunaCalculation
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  height: 100vh;
}

.logo{
  height: 100px;
  display: flex;
  justify-content: center;
  width: 100%;
}
</style>
