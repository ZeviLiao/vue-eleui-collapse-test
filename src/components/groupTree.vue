<template>
  <div>
    {{ allCheckIds }}
    <div v-for="(data, i) in treeData" :key="i">
      <GroupTreeItem
        v-model="checkIds[i]"
        :data="[data]"
        :dataUnBind="data.dataUnBind"
      />
    </div>
  </div>
</template>

<script>
import GroupTreeItem from "./groupTreeItem.vue";
export default {
  components: {
    GroupTreeItem
  },
  props: ["treeData"],
  data() {
    return {
      checkIds: [[]]
    };
  },
  methods: {
    // checkChange(val) {
    //   this.checkIds = val;
    //   console.log(this.checkIds);
    // }
  },
  computed: {
    allCheckIds() {
      return this.checkIds.flat();
    }
  }
};
</script>

<style lang="scss" scoped></style>
