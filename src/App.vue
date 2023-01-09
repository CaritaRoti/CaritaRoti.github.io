<template>
  <header>
    <h1>
      Curiosity<span>Cam</span>
    </h1>
  </header>
  <CuriosityCamera />
</template>

<script>
import CuriosityCamera from './components/CuriosityCamera.vue'

export default {
  name: 'App',
  components: {
    CuriosityCamera
  }
}
</script>

<style scoped>
header {
  line-height: 1.5;
  font-size: large;
  font-weight: 300;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0;
  margin-bottom: 1%;
  padding: 0;
}

header h1 {
  color: #41b883;
}

header h1 span {
  color: #d0d0d0;
  font-weight: 400;
}
</style>
