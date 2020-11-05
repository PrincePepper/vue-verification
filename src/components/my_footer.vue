<template>
  <div class="inner">
    <p>Copyright &copy; <a href="https://ssereda.ru/">Semen Sereda</a></p>
  </div>
</template>

<script>
export default {
  name: "footer"
}
</script>

<style scoped>
.inner {
  color: #999; /* IE8 proofing */
  color: rgba(255, 255, 255, .5);
  background-color: #9a63ff;
  text-align: center;
  padding: 16px;
}

a,
a:focus,
a:hover {
  color: #ffffff;
  transition: 0.2s;
  -moz-transition: 0.2s;
  -webkit-transition: 0.2s;
  -o-transition: 0.2s;
}
</style>
