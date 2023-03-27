<template>
  <div class="container">
    <div class="wrapper">
      <StopWatch />
    </div>
  </div>
</template>
<script>
import StopWatch from "./components/StopWatch.vue";
export default {
  name: "App",
  components: {
    StopWatch,
  },
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  background: #3b3b3b;
}
.container {
  width: 70%;
  margin: 75px auto;
}
.wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 52px;
}
/* responsive */
@media (max-width: 768px) {
  .wrapper {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-gap: 50px;
  }
}

@media (max-width: 576px) {
  .wrapper {
    display: grid;
    grid-template-columns: 1fr;
    grid-gap: 45px;
  }
}
/* end */
</style>
