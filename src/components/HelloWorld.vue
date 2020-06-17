<template>
  <div>
    <div @click="cb">
      <i
        class="el-collapse-item__arrow el-icon-arrow-down"
        :class="{ 'is-active': show }"
      ></i>
    </div>

    <div style="width:50%;margin: 0 auto;">
      <el-collapse-transition>
        <div v-if="show" class="testshow">
          <div>sssssss</div>
          <div>sssssss</div>
          <div>sssssss</div>
          <div>sssssss</div>
          <div>sssssss</div>
        </div>
      </el-collapse-transition>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    show: false
  }),
  methods: {
    cb() {
      this.show = !this.show;
    }
  }
};
</script>
<style lang="scss" scoped>
.testshow {
  padding: 10px 10px;
  background-color: aqua;
}

.el-collapse-item__arrow.is-active {
  transform: rotate(-180deg);
}
</style>
