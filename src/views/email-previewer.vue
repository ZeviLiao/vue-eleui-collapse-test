<template>
  <el-dialog
    :visible="visible"
    :title="'email.notify_preview'"
    :close-on-press-escape="false"
    :close-on-click-modal="false"
    :lock-scroll="true"
    :append-to-body="true"
    custom-class="notify-email-previewer"
    width="800px"
    @close="close"
  >
    <div class="email-container">
      <!-- 邮件标题 -->
      <h3>{{'email.text_title'}}</h3>
      <p class="email-title" v-html="replaceText(data.title)"></p>
      <h3 style="margin-top: 24px;">{{'email.text_content'}}</h3>
      <!-- 邮件正文 -->
      <div class="email-content">
        <!-- 通知类型 -->
        <h4 class="notify-type-text">{{data.formTitle}}:</h4>
        <p class="email-message" v-html="replaceText(data.message)"></p>
        <regist-previewer v-if="data.attachment" :data="visitorRegistTemplate"></regist-previewer>
        <!-- 请勿回复提示 -->
        <p class="email-tips">{{'email.content_tips_not_reply'}}</p>
      </div>
      <!-- 页脚 -->
      <div class="email-footer">
        <div class="nuwa-email-logo">
          <img :src="`/public/static/images/mail-logo.png`" width="139" height="10" alt />
        </div>
      </div>
    </div>
  </el-dialog>
</template>
<script>
// import { emailVariables } from './variables'
import RegistPreviewer from "./regist-previewer";
export default {
  components: {
    RegistPreviewer,
  },
  props: {
    visible: Boolean,
  },
  data() {
    return {
      data: {
        title: "title",
        formTitle: "formTitle",
        message: "message",
        attachment: false,
      },
      visitorRegistTemplate: {
        ver: "1",
        visitorInfo: {
          visitorName: "email.template_person_name",
          intervieweeName: "email.template_person_name_2",
          purposeOfVisit: "1",
          purposeRemark: "",
          visitorStatus: "2",
          statusRemark: "",
        },
        healthQuestionnaire: {
          systemicSymptoms: ["0"],
          digestiveSymptoms: ["0"],
          respiratorySymptoms: ["0"],
        },
        createdAt: "2020-12-18T07:03:47.417Z",
      },
    };
  },
  methods: {
    replaceText(text) {
      // const variables = emailVariables(this.data.notifyType)
      // variables.forEach(item => {
      //     const reg = new RegExp(item.reg, 'gm')
      //     text = text.replace(reg, item.htmlText)
      // })
      // return text
      return text;
    },
    close() {
      this.$emit("update:visible", false);
    },
  },
};
</script>
<style lang="scss">
$--color-primary: blue;
.notify-email-previewer {
  .el-dialog__header {
    padding: 24px 55px 10px 55px;
  }
  .el-dialog__body {
    padding: 0;
    padding-bottom: 24px;
  }
  .email-container {
    padding: 0 55px;
    h3 {
      padding-bottom: 12px;
      font-size: 16px;
      font-weight: normal;
      color: #333;
      line-height: 32px;
    }
    .email-title {
      width: 100%;
      padding: 0 10px;
      line-height: 48px;
      font-size: 20px;
      color: #333;
      border-radius: 7px;
      border: solid 1px rgba(0, 181, 226, 0.1);
    }
    .email-content {
      max-height: 320px;
      overflow: auto;
      padding: 18px 24px;
      border-top: 5px solid $--color-primary;
    }
    .notify-type-text {
      font-size: 24px;
      padding: 12px 0;
      font-weight: normal;
      color: #333;
    }
    .email-message {
      margin-top: 12px;
      line-height: 1.75em;
      font-size: 15px;
      color: #333;
    }
    .email-tips {
      margin-top: 50px;
      font-size: 12px;
      line-height: 32px;
      color: #4a4a4a;
      text-align: center;
    }
    .email-footer {
      width: 100%;
      height: 30px;
      background: rgba(26, 201, 245, 0.1);
      color: #4a4a4a;
      text-align: center;
      .nuwa-webs {
        line-height: 60px;
      }
      .nuwa-email-logo {
        width: 100%;
        height: 30px;
        line-height: 30px;
        font-size: 0;
        background: $--color-primary;
        img {
          vertical-align: middle;
        }
      }
    }
  }
}
</style>
