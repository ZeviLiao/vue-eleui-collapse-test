<template>
  <div>
    <el-tree
      :data="data"
      show-checkbox
      default-expand-all
      node-key="id"
      ref="tree"
      highlight-current
      @check="onChange"
    ></el-tree>

    <accordion :dataUnBind="dataUnBind"></accordion>
  </div>
</template>

<script>
import Accordion from "./accordion";
export default {
  props: ["checkIds", "data", "dataUnBind"],
  model: {
    prop: "checkIds",
    event: "change"
  },
  methods: {
    onChange() {
      this.$emit("change", this.$refs.tree.getCheckedKeys(true));
    }
  },
  components: {
    Accordion
  },
  watch: {
    checkIds: {
      handler(val) {
        this.$refs.tree.setCheckedKeys(val);
      },
      deep: true
    }
  }
};
</script>

<style lang="scss" scoped></style>
