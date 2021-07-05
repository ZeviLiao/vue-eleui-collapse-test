<template>
  <div>
    <el-collapse v-model="activeNames" @change="handleChange">
      <el-collapse-item name="1">
        <span class="collapse-title" slot="title">Consistency Consistency</span>
        <div>
          Consistent with real life: consistent with the process and logic of
          real life, and follow the language and concepts that users are used
          to;
        </div>
        <div>
          Consistent in the interface: All elements and structures must be
          consistent, such as: design style, icon and text, element location,
          etc.
        </div>
      </el-collapse-item>
      <el-collapse-item name="2">
        <span class="collapse-title" slot="title">Feedback Feedback</span>
        <div>
          Control feedback: through interface styles and interactive dynamic
          effects, users can clearly perceive their operations;
        </div>
        <div>
          Page feedback: After the operation, the current status is clearly
          displayed through the changes of page elements.
        </div>
      </el-collapse-item>
      <el-collapse-item name="3">
        <span class="collapse-title" slot="title">Efficiency Efficiency</span>
        <div>
          Simplified process: design a simple and intuitive operation process;
        </div>
        <div>
          Clear and clear: the language is clear and the meaning is clear,
          allowing users to quickly understand and make decisions;
        </div>
        <div>
          Help users to identify: The interface is simple and straightforward,
          allowing users to quickly identify rather than recall, reducing the
          user's memory burden.
        </div>
      </el-collapse-item>
      <el-collapse-item name="4">
        <span class="collapse-title" slot="title">Controllability</span>
        <div>
          User decision-making: According to the scene, the user can be given
          operation suggestions or safety tips, but it cannot replace the user
          in making decisions;
        </div>
        <div>
          Controllable results: users can freely perform operations, including
          undo, rollback, and termination of current operations.
        </div>
      </el-collapse-item>
    </el-collapse>
  </div>
</template>

<script>
export default {};
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
