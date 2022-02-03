<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <h3>Hello World</h3>
    <Counter />
  </div>
</template>

<script>
// @ is an alias to /src
import Counter from "@/components/Counter.vue";
export default {
  name: "Home",
  components: {
    Counter,
  },
};
</script>
