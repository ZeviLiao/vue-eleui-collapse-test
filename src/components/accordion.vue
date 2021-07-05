<template>
  <div>
    <el-collapse @change="handleChange">
      <el-collapse-item name="1">
        <span class="collapse-title" slot="title">Consistency Consistency</span>
        <span v-for="(n, i) in dataUnBind" :key="i">{{ n }}&nbsp;&nbsp;</span>
      </el-collapse-item>
    </el-collapse>
  </div>
</template>

<script>
export default {
  props: ["dataUnBind"],
  methods: {
    handleChange() {}
  }
};
</script>

<style lang="scss" scoped>
.collapse-title {
  flex: 1 0 90%;
  order: 1;
}

.el-collapse-item__header {
  flex: 1 0 auto;
  order: -1;
}
</style>
