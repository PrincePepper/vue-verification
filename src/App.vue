<template>
  <div id="app">
    <jumbotron id="jumbotron"/>
    <div id="main" class="container">
      <div class="row">
        <div class="col-3"></div>
        <div class="col-6">
          <my_forms id="my_forms"/>
        </div>
        <div class="col-3"></div>
      </div>
    </div>
    <my_footer/>
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

import jumbotron from "@/components/jumbotron";
import my_footer from "@/components/my_footer";
import my_forms from "@/components/my_forms";

export default {
  name: 'App',
  components: {
    jumbotron, my_footer, my_forms
  }
}
</script>

<style>
#app {
  font-family: Forward, Helvetica, "Montserrat Medium", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 0;
  background-color: #9a63ff;

  display: flex;
  flex-direction: column;
  min-height: 100%;
}

html {
  height: 100%;
}

body {
  height: 100%;
}

#main {
  flex: 1 0 auto;
  padding: inherit;
}
</style>
