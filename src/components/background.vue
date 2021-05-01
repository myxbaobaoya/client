<template>
    <div id="background">
      <vue-particles
        id="particles-js"
        color="#fff"
        :particleOpacity="0.7"
        :particlesNumber="60"
        shapeType="circle"
        :particleSize="4"
        linesColor="#fff"
        :linesWidth="1"
        :lineLinked="true"
        :lineOpacity="0.4"
        :linesDistance="150"
        :moveSpeed="2"
        :hoverEffect="true"
        hoverMode="grab"
        :clickEffect="true"
        clickMode="push"
        class="lizi"
      >
      </vue-particles>
    </div>
</template>

<script>
export default {
  name: 'background',
};
</script>

<style scoped>
#background {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #4a5010;
    background: #191919;  /* margin-top: 60px; */
  }
</style>
