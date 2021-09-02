<template>
  <div class="container">
    <Indecision/>
  </div>
  <!--
  <Counter title="Entraron"/>
  <Counter :start="5" title="Salieron"/>
  <Counter :start="15"/>
  -->
</template>

<script>
import Indecision from '@/components/Indecision.vue'
export default {
  name: 'App',
  components: {
    Indecision
  }
}
</script>

<style>
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
body {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  /*background: black;*/
  background-color: rgb(16, 11, 11);
  border: solid 1px rgb(15, 14, 14);
  box-shadow:
    inset 45px 0px 180px #f0f,
    inset -48px -60px 180px #0ff;
  font-family: 'Helvetica';
}
.container{
  display: flex;
  justify-content: center;
  align-content: center;
}



</style>
