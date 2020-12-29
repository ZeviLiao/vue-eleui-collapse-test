<template>
  <div class="email-container">
    <!-- 邮件标题 -->
    <h3>標題主旨：</h3>
    <p class="email-title" v-html="email && email.title"></p>
    <h3 style="margin-top: 24px;">內文：</h3>
    <!-- 邮件正文 -->
    <div class="email-content">
      <!-- 通知类型 -->
      <h4 class="notify-type-text">來訪通知：</h4>
      <p class="email-message" v-html="email && email.message"></p>
      <!-- <regist-previewer v-if="data.attachment" :data="visitorRegistTemplate"></regist-previewer> -->
      <!-- 请勿回复提示 -->
      <p class="email-tips">*注意: 此封信由系統發送，請勿回覆此 Email</p>
    </div>
    <!-- 页脚 -->
    <div class="email-footer">
      <div class="nuwa-email-logo">
        <img :src="`/public/static/images/mail-logo.png`" width="139" height="10" alt />
      </div>
    </div>
  </div>
</template>
<script>
// import { emailVariables } from './variables'
// import RegistPreviewer from "./regist-previewer";
import hb from "handlebars";

export default {
  mounted() {
    this.scenario = {
      name: "xxx", //場景名稱
      receptionMessage: "口罩不離身，隨時勤洗手，病毒遠離你。", //接待語
      temperature: {
        //溫度設定
        mode: 1, //溫度測定模式，1-複測模式（紅外線＋熱顯像測溫），2-精準模式（紅外線測溫），3-快篩模式（熱顯像測溫）
        unit: "c", //溫度單位， c-攝氏，f-華氏
        value: 37.5, //示警溫度值
        reTestMessage: "體溫有點高，不舒服的話要去看醫生，多喝水、多休息。", //溫度測試完畢結語
      },
      devices: [
        //關連設備
        {
          sn: "xxx",
        },
      ],
      people: [
        {
          //關連人群
          personId: "9gss25bQ9zR1L1LW", //人員Id
        },
      ],
      maintainers: [
        {
          //維護者名單
          name: "lzk", //維護者名稱
          email: "luo.zhikai@nuwarobotics.com", //維護者郵箱
          isDefault: true, //是否是默認存在的，默認存在的維護者不可刪除
          characters: [
            {
              //角色設定，陌生人為默認設定
              i18n: [
                //用於顯示維護者標題的-頁面沒有可設置的地方，只能系統去判斷取名
                { langCode: "zh-TW", name: "維護者一號" },
              ],
              characterId: "xxoo", //角色id
              characterType: "stranger", //角色類型，stranger-陌生人，character-已設定的角色
              characterName: "陌生人", //角色名稱
              //需要通知的事件，normalTemperature-溫度正常，abnormalTemperature-溫度異常, noMask-沒戴口罩, visiting-來訪
              notifies: ["abnormalTemperature", "noMask", "visiting"],
            },
            {
              //角色設定，根據已設定角色設置
              characterId: "xxpp", //角色id
              characterType: "character", //角色類型，stranger-陌生人，character-已設定的角色
              characterName: "老闆娘", //角色名稱
              notifies: ["abnormalTemperature", "noMask", "visiting"],
            },
          ],
        },
      ],
      emails: [
        //郵件設定

        //通知類型, noMask-沒戴口罩， abnormalTemperature-溫度異常， normalTemperature-溫度正常， visiting-來訪
        {
          notifyType: "noMask",
          i18n: [
            {
              //用於顯示郵件標題的
              langCode: "zh-TW",
              name: "陌生人來訪通知",
            },
          ],
          title: "【女媧接待系統】 -  %character %name 來訪通知 %time", //郵件內容標題
          message: "%character %name 來訪，詳細目的如下附件：", //郵件內容正文
          attachment: "xx", //附件的表格id
        },
        {
          //溫度正常通知
          notifyType: "normalTemperature",
          i18n: [
            {
              langCode: "zh-TW",
              name: "體溫異常通知",
            },
          ],
          title: "【女媧接待系統】 -  %time %name 體溫異常通知",
          message:
            "體溫異常通知\n%time %name%salutation%\n體溫：%temperature°C\n%noFaceMask',",
          attachment: null,
        },
        {
          //溫度異常通知
          notifyType: "abnormalTemperature",
          i18n: [
            {
              langCode: "zh-TW",
              name: "體溫異常通知",
            },
          ],
          title: "【女媧接待系統】 -  %time %name 體溫異常通知",
          message:
            "體溫異常通知\n%time %name%salutation%\n體溫：%temperature°C\n%noFaceMask',",
          attachment: null,
        },
        {
          //角色訪問通知
          notifyType: "visiting",

          i18n: [
            {
              langCode: "zh-TW",
              name: "體溫異常通知",
            },
          ],
          title: "【女媧接待系統】 -  %time %name 體溫異常通知",
          message:
            "體溫異常通知\n%time %name%salutation%\n體溫：%temperature°C\n%noFaceMask',",
          attachments: [
            {
              notifyType: "stranger",
              attachment: "xxx",
            },
            {
              notifyType: "character",
              characterId: "xxx", //角色的id
              attachment: "xxx",
            },
          ],
        },
      ],
    };
    this.email = this.scenario.emails.find(
      (o) => o.notifyType === this.notifyType
    );
    let userData = {
      time: "2020/1/1 6:23 pm",
      name: "Zevi",
      salutation: "good",
      temperature: "36.5",
      noFaceMask: true,
    };
    this.email.title = this.convertTemplate(this.email.title, userData);
    this.email.message = this.convertTemplate(this.email.message, userData);
  },
  components: {
    // RegistPreviewer,
  },
  props: {},
  data() {
    return {
      scenario: {},
      notifyTypeOpts: [
        "noMask",
        "abnormalTemperature",
        "normalTemperature",
        "visiting",
      ],
      notifyType: "visiting",
      langCode: "zh-TW",
      email: {},
      vvisible: true,
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
    convertTemplate(text, userData) {
      let arrVars = Object.keys(userData);
      const buildRegs = (arr) => {
        return arr.map((v) => {
          return { reg: `%(${v})`, value: "{{$1}}" };
        });
      };
      let variables = buildRegs(arrVars);
      variables.push({ reg: "\n", value: "<br/>" }); // enter

      variables.forEach((item) => {
        const regex = new RegExp(item.reg, "gm");
        text = text.replace(regex, item.value);
      });

      var template = hb.compile(text);
      return template(userData);
    },

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
