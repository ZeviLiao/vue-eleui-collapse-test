<template>
  <div class="visitor-regist-previewer">
    <h3 class="form-title">訪客基本資訊</h3>
    <div class="form-content" v-html="showAttach">
      <!-- <p class="form-item-row">
        <span class="prop-label">來訪者姓名</span>
        <span class="prop-value">{{dataInfo.attachment.visitorName}}</span>
      </p>
      <p class="form-item-row">
        <span class="prop-label">受訪者姓名</span>
        <span class="prop-value">{{dataInfo.attachment.respondentName}}</span>
      </p>
      <p class="form-item-row">
        <span class="prop-label">探訪目的</span>
        <span
          class="prop-value"
        >{{dataInfo.attachment.reason}}：{{dataInfo.attachment.reasonNote}}</span>
      </p>
      <p class="form-item-row">
        <span class="prop-label">來訪身份</span>
        <span
          class="prop-value"
        >{{dataInfo.attachment.characterName}}：{{dataInfo.attachment.characterNote}}</span>
      </p>-->
    </div>
    <h3 class="form-title">身體狀況調查表</h3>
    <div class="form-content" v-html="showHealth">
      <!-- <p class="form-item-row">
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
      </p>-->
    </div>
  </div>
</template>
<script>
/**
 * 訪客登記表預覽
 */
// import Vue from "vue";
// const $t = (key, value) => Vue.prototype.$t(key, value);

import hb from "handlebars";

export default {
  mounted() {
    this.showAttach = this.buildHtmlList(this.dataInfo.attachment);
    this.showHealth = this.buildHtmlList(this.dataInfo.health);
  },
  data() {
    return {
      // dataInfo.attachment[0].visitorName

      rowTemp: `<p class="form-item-row">
          <span class="prop-label">{{key}}</span>
          <span class="prop-value">{{value}}</span>
        </p>`,
      showAttach: "",
      showHealth: "",
    };
  },
  props: {
    dataInfo: {
      type: Object,
    },
  },
  methods: {
    buildHtmlList(src) {
      let str = "";
      var template = hb.compile(this.rowTemp);
      Object.keys(src).forEach(
        (item) =>
          (str += template({
            key: item,
            value: src[item],
          }))
      );
      return str;
    },
  },
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
