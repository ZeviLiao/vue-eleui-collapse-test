<template>
  <div class="visitor-regist-previewer">
    <h3 class="form-title">訪客基本資訊</h3>
    <div class="form-content">
      <p class="form-item-row">
        <span class="prop-label">來訪者姓名</span>
        <span class="prop-value">{{dataInfo.attachment[0].visitorName}}</span>
      </p>
      <p class="form-item-row">
        <span class="prop-label">受訪者姓名</span>
        <span class="prop-value">{{dataInfo.attachment[0].visitorName}}</span>
      </p>
      <p class="form-item-row">
        <span class="prop-label">探訪目的</span>
        <span
          class="prop-value"
        >{{dataInfo.attachment[0].reason}}：{{dataInfo.attachment[0].reasonNote}}</span>
      </p>
      <p class="form-item-row">
        <span class="prop-label">來訪身份</span>
        <span
          class="prop-value"
        >{{dataInfo.attachment[1].characterName}}：{{dataInfo.attachment[1].characterNote}}</span>
      </p>
    </div>
    <h3 class="form-title">身體狀況調查表</h3>
    <div class="form-content">
      <p class="form-item-row">
        <span class="prop-label">全身症狀</span>
        <span class="prop-value">{{dataInfo.health.body[0]}}</span>
      </p>
      <p class="form-item-row">
        <span class="prop-label">消化道症狀</span>
        <span
          class="prop-value"
        >{{dataInfo.health.digestiveTrack[0]}}、{{dataInfo.health.digestiveTrack[1]}}</span>
      </p>
      <p class="form-item-row">
        <span class="prop-label">呼吸道症狀</span>
        <span class="prop-value">{{dataInfo.health.respiratoryTrack[0]}}</span>
      </p>
    </div>
  </div>
</template>
<script>
/**
 * 訪客登記表預覽
 */
// import Vue from "vue";
// const $t = (key, value) => Vue.prototype.$t(key, value);
export default {
  props: {
    dataInfo: {
      type: Object
    },
  },
  methods: {},
};
</script>
<style lang="scss">
.visitor-regist-previewer {
  .form-title {
    padding: 18px 0;
    font-size: 16px;
    font-weight: bold;
    color: #333;
  }
  .form-content {
    padding: 0 15px;
    border-radius: 5px;
    background-color: rgba(154, 206, 215, 0.1);
    .form-item-row {
      width: 100%;
      padding: 12px 4px;
      font-size: 14px;
      color: #333;
      line-height: 1.5em;
      border-bottom: solid 1px rgba(0, 181, 226, 0.1);
      display: flex;
      justify-content: flex-start;
      align-items: center;
      &:last-child {
        border-bottom: none;
      }
      .prop-label {
        width: 120px;
        flex: 0 0 auto;
      }
      .prop-value {
        flex: 1 1 auto;
        padding-left: 14px;
      }
    }
  }
}
</style>
