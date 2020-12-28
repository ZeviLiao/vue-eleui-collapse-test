<template>
    <div class="visitor-regist-previewer">
        <h3 class="form-title">
            {{$t('report_all.visitor_info')}}
        </h3>
        <div class="form-content">
            <p class="form-item-row">
                <span class="prop-label">{{$t('visitor_form.prop_visitor_name')}}</span>
                <span class="prop-value">{{data.visitorInfo.visitorName}}</span>
            </p>
            <p class="form-item-row">
                <span class="prop-label">{{$t('visitor_form.prop_interviewee_name')}}</span>
                <span class="prop-value">{{data.visitorInfo.intervieweeName}}</span>
            </p>
            <p class="form-item-row">
                <span class="prop-label">{{$t('visitor_form.prop_purpose_visit')}}</span>
                <span class="prop-value">
                    {{data.visitorInfo.purposeOfVisit | getSingleSelectionLabel('purpose_visit_', data.visitorInfo.purposeRemark)}}
                </span>
            </p>
            <p class="form-item-row">
                <span class="prop-label">{{$t('visitor_form.prop_visitor_status')}}</span>
                <span class="prop-value">
                    {{data.visitorInfo.visitorStatus | getSingleSelectionLabel('visitor_status_', data.visitorInfo.statusRemark)}}
                </span>
            </p>
        </div>
        <h3 class="form-title">
            {{$t('visitor_form.title_health_report')}}
        </h3>
        <div class="form-content">
            <p class="form-item-row">
                <span class="prop-label">{{$t('visitor_form.prop_system_symptoms')}}</span>
                <span class="prop-value">{{data.healthQuestionnaire.systemicSymptoms | getMultiSelectionLabel('systemic_symptoms_')}}</span>
            </p>
            <p class="form-item-row">
                <span class="prop-label">{{$t('visitor_form.digestive_symptoms')}}</span>
                <span class="prop-value">{{data.healthQuestionnaire.digestiveSymptoms | getMultiSelectionLabel('digestive_symptoms_')}}</span>
            </p>
            <p class="form-item-row">
                <span class="prop-label">{{$t('visitor_form.respiratory_symptoms')}}</span>
                <span class="prop-value">{{data.healthQuestionnaire.respiratorySymptoms | getMultiSelectionLabel('respiratory_symptoms_')}}</span>
            </p>
        </div>
    </div>
</template>
<script>
/**
 * 訪客登記表預覽
 */
import Vue from 'vue'
const $t = (key, value) => Vue.prototype.$t(key, value)
export default {
    props: {
        data: {
            type: Object,
            default () {
                return {
                    'ver': '1',
                    'visitorInfo': {
                        'visitorName': '',
                        'intervieweeName': '',
                        'purposeOfVisit': '',
                        'purposeRemark': '',
                        'visitorStatus': '',
                        'statusRemark': ''
                    },
                    'healthQuestionnaire': {
                        'systemicSymptoms': [],
                        'digestiveSymptoms': [],
                        'respiratorySymptoms': []
                    },
                    'createdAt': '2020-12-18T07:03:47.417Z'
                }
            }
        }
    },
    filters: {
        // 獲取基本資料單選文本
        getSingleSelectionLabel (value, keyPrefix, remark) {
            if (value === '50') {
                return `${$t('regist_option.text_selected_others')}:${remark}`
            }
            return $t(`regist_option.${keyPrefix}${value}`)
        },
        // 獲取身體狀況多選項文本
        getMultiSelectionLabel (value = [], keyPrefix = '') {
            let arr = value.map(item => {
                if (item === '0') {
                    return $t('regist_option.text_selected_none')
                } else {
                    return $t(`regist_option.${keyPrefix}${item}`)
                }
            })
            return arr.join(',')
        }
    },
    methods: {
        a (aa, bbb) {

        }
    }
}
</script>
<style lang="scss">
.visitor-regist-previewer{
    .form-title{
        padding: 18px 0;
        font-size: 16px;
        font-weight: bold;
        color: #333;
    }
    .form-content{
        padding: 0 15px;
        border-radius: 5px;
        background-color: rgba(154, 206, 215, 0.1);
        .form-item-row{
            width: 100%;
            padding: 12px 4px;
            font-size: 14px;
            color: #333;
            line-height: 1.5em;
            border-bottom: solid 1px rgba(0, 181, 226, 0.1);
            display: flex;
            justify-content: flex-start;
            align-items: center;
            &:last-child{
                border-bottom: none;
            }
            .prop-label{
                width: 120px;
                flex: 0 0 auto;
            }
            .prop-value{
                flex: 1 1 auto;
                padding-left: 14px;
            }
        }
    }
}
</style>
