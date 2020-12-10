<template>
  <div class="jumbotron">
    <h1 class="display-1">Привет, Друг!</h1>
    <p class="lead">Работа с <kbd class="first_">vue.js</kbd> и <kbd class="second_">form</kbd></p>
  </div>
</template>

<script>
export default {
  name: "jumbotron"
}
</script>

<style scoped>
.jumbotron {
  background-color: #9100FE;
  padding: 0;
  color: white;
}

.first_ {
  background-color: #41b783;
  font-size: 1.5vmax;
  font-weight: bold;
}

.second_ {
  background-color: #FF8300;
  font-size: 1.5vmax;
  font-weight: bold;
}
</style>
