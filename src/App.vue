<template>
  <div id="app">
    <!-- <h1>{{ message }}</h1> -->
    <!-- <element-view></element-view> -->
    <!-- <emp-view></emp-view> -->
    <router-view></router-view>
  </div>
</template>

<script>
// import EmpView from './views/tilas/EmpView.vue'
// import ElementView from './views/element/ElementView.vue'
export default {
  // components: { EmpView },
  // components: { ElementView },
  data() {
    return {
      message: "Hello Vue"
    }
  }
}
</script>

<style></style>
