<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png" /> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    <div style="width:300px">
      <Accordion />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
import Accordion from "@/components/accordion.vue";

export default {
  name: "Home",
  components: {
    // HelloWorld,
    Accordion
  }
};
</script>
