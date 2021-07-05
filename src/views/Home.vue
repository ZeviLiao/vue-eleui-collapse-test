<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png" /> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    <div style="width:300px">
      <!-- <Accordion /> -->
      <GroupTree :treeData="treeData" />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
// import Accordion from "@/components/accordion.vue";
import GroupTree from "@/components/groupTree.vue";

export default {
  name: "Home",
  data() {
    return {
      treeData: [
        {
          id: 1,
          label: "Level one 1",
          children: [
            {
              id: 9,
              label: "Level three 1-1-1"
            },
            {
              id: 10,
              label: "Level three 1-1-2"
            }
          ],
          dataUnBind: ["aa", "bb", "cc"]
        },
        {
          id: 2,
          label: "Level one 2",
          children: [
            {
              id: 19,
              label: "Level three 1-2-1"
            },
            {
              id: 20,
              label: "Level three 1-2-2"
            }
          ],
          dataUnBind: ["aa1", "bb1", "cc1"]
        }
      ]
    };
  },
  components: {
    // HelloWorld,
    // Accordion,
    GroupTree
  }
};
</script>
