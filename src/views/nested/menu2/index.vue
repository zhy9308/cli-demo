<template>
  <div class="test-form">
    <parser :form-conf="formConf" @submit="sumbitForm1" />
    <parser :key="key2" :form-conf="formConf" @submit="sumbitForm2" />
    <el-button @click="change">
      change
    </el-button>
  </div>
</template>

<script>
// import Parser from '../Parser'
// 若parser是通过安装npm方式集成到项目中的，使用此行引入
import Parser from 'form-gen-parser'
export default {
  components: {
    Parser
  },
  props: {},
  data() {
    return {
      key2: +new Date(),
      formConf: {
  "fields": [{
    "__config__": {
      "label": "级联选择",
      "showLabel": true,
      "labelWidth": null,
      "tag": "el-cascader",
      "tagIcon": "cascader",
      "layout": "colFormItem",
      "defaultValue": [],
      "dataType": "dynamic",
      "span": 12,
      "required": true,
      "regList": [],
      "changeTag": true,
      "document": "https://element.eleme.cn/#/zh-CN/component/cascader",
      "formId": 101,
      "renderKey": 1589015572257
    },
    "options": [{
      "id": 1,
      "value": 1,
      "label": "选项1",
      "children": [{
        "id": 2,
        "value": 2,
        "label": "选项1-1"
      }]
    }],
    "placeholder": "请选择级联选择",
    "style": {
      "width": "100%"
    },
    "props": {
      "props": {
        "multiple": false,
        "label": "label",
        "value": "value",
        "children": "children"
      }
    },
    "show-all-levels": true,
    "disabled": false,
    "clearable": true,
    "filterable": false,
    "separator": "/",
    "__vModel__": "field101"
  }, {
    "__config__": {
      "label": "多选框组",
      "tag": "el-checkbox-group",
      "tagIcon": "checkbox",
      "defaultValue": [],
      "span": 12,
      "showLabel": true,
      "labelWidth": null,
      "layout": "colFormItem",
      "optionType": "default",
      "required": true,
      "regList": [],
      "changeTag": true,
      "border": false,
      "document": "https://element.eleme.cn/#/zh-CN/component/checkbox",
      "formId": 102,
      "renderKey": 1589015579443
    },
    "__slot__": {
      "options": [{
        "label": "选项一",
        "value": 1
      }, {
        "label": "选项二",
        "value": 2
      }]
    },
    "style": {},
    "size": "medium",
    "disabled": false,
    "__vModel__": "field102"
  }, {
    "__config__": {
      "label": "级联选择",
      "showLabel": true,
      "labelWidth": null,
      "tag": "el-cascader",
      "tagIcon": "cascader",
      "layout": "colFormItem",
      "defaultValue": [],
      "dataType": "dynamic",
      "span": 12,
      "required": true,
      "regList": [],
      "changeTag": true,
      "document": "https://element.eleme.cn/#/zh-CN/component/cascader",
      "formId": 103,
      "renderKey": 1589015901535
    },
    "options": [{
      "id": 1,
      "value": 1,
      "label": "选项1",
      "children": [{
        "id": 2,
        "value": 2,
        "label": "选项1-1"
      }]
    }],
    "placeholder": "请选择级联选择",
    "style": {
      "width": "100%"
    },
    "props": {
      "props": {
        "multiple": false,
        "label": "label",
        "value": "value",
        "children": "children"
      }
    },
    "show-all-levels": true,
    "disabled": false,
    "clearable": true,
    "filterable": false,
    "separator": "/",
    "__vModel__": "field103"
  }, {
    "__config__": {
      "label": "滑块",
      "tag": "el-slider",
      "tagIcon": "slider",
      "defaultValue": 0,
      "span": 12,
      "showLabel": true,
      "layout": "colFormItem",
      "labelWidth": null,
      "required": true,
      "regList": [],
      "changeTag": true,
      "document": "https://element.eleme.cn/#/zh-CN/component/slider",
      "formId": 104,
      "renderKey": 1589015903039
    },
    "disabled": false,
    "min": 0,
    "max": 100,
    "step": 1,
    "show-stops": false,
    "range": false,
    "__vModel__": "field104"
  }, {
    "__config__": {
      "label": "单行文本",
      "labelWidth": null,
      "showLabel": true,
      "changeTag": true,
      "tag": "el-input",
      "tagIcon": "input",
      "required": true,
      "layout": "colFormItem",
      "span": 12,
      "document": "https://element.eleme.cn/#/zh-CN/component/input",
      "regList": [],
      "formId": 106,
      "renderKey": 1589017002439
    },
    "__slot__": {
      "prepend": "",
      "append": ""
    },
    "placeholder": "请输入单行文本",
    "style": {
      "width": "100%"
    },
    "clearable": true,
    "prefix-icon": "",
    "suffix-icon": "",
    "maxlength": null,
    "show-word-limit": false,
    "readonly": false,
    "disabled": false,
    "__vModel__": "field106"
  }, {
    "__config__": {
      "label": "密码",
      "showLabel": true,
      "labelWidth": null,
      "changeTag": true,
      "tag": "el-input",
      "tagIcon": "password",
      "layout": "colFormItem",
      "span": 12,
      "required": true,
      "regList": [],
      "document": "https://element.eleme.cn/#/zh-CN/component/input",
      "formId": 107,
      "renderKey": 1589018101778
    },
    "__slot__": {
      "prepend": "",
      "append": ""
    },
    "placeholder": "请输入密码",
    "show-password": true,
    "style": {
      "width": "100%"
    },
    "clearable": true,
    "prefix-icon": "",
    "suffix-icon": "",
    "maxlength": null,
    "show-word-limit": false,
    "readonly": false,
    "disabled": false,
    "__vModel__": "field107"
  }, {
    "__config__": {
      "label": "级联选择",
      "showLabel": true,
      "labelWidth": null,
      "tag": "el-cascader",
      "tagIcon": "cascader",
      "layout": "colFormItem",
      "defaultValue": [],
      "dataType": "dynamic",
      "span": 12,
      "required": true,
      "regList": [],
      "changeTag": true,
      "document": "https://element.eleme.cn/#/zh-CN/component/cascader",
      "formId": 108,
      "renderKey": 1589018103889
    },
    "options": [{
      "id": 1,
      "value": 1,
      "label": "选项1",
      "children": [{
        "id": 2,
        "value": 2,
        "label": "选项1-1"
      }]
    }],
    "placeholder": "请选择级联选择",
    "style": {
      "width": "100%"
    },
    "props": {
      "props": {
        "multiple": false,
        "label": "label",
        "value": "value",
        "children": "children"
      }
    },
    "show-all-levels": true,
    "disabled": false,
    "clearable": true,
    "filterable": false,
    "separator": "/",
    "__vModel__": "field108"
  }, {
    "__config__": {
      "label": "计数器",
      "showLabel": true,
      "changeTag": true,
      "labelWidth": null,
      "tag": "el-input-number",
      "tagIcon": "number",
      "span": 12,
      "layout": "colFormItem",
      "required": true,
      "regList": [],
      "document": "https://element.eleme.cn/#/zh-CN/component/input-number",
      "formId": 105,
      "renderKey": 1589017001191
    },
    "placeholder": "计数器",
    "step": 1,
    "step-strictly": false,
    "controls-position": "",
    "disabled": false,
    "__vModel__": "field105"
  }, {
    "__config__": {
      "label": "时间范围",
      "tag": "el-time-picker",
      "tagIcon": "time-range",
      "span": 12,
      "showLabel": true,
      "labelWidth": null,
      "layout": "colFormItem",
      "defaultValue": null,
      "required": true,
      "regList": [],
      "changeTag": true,
      "document": "https://element.eleme.cn/#/zh-CN/component/time-picker",
      "formId": 110,
      "renderKey": 1589018106473
    },
    "style": {
      "width": "100%"
    },
    "disabled": false,
    "clearable": true,
    "is-range": true,
    "range-separator": "至",
    "start-placeholder": "开始时间",
    "end-placeholder": "结束时间",
    "format": "HH:mm:ss",
    "value-format": "HH:mm:ss",
    "__vModel__": "field110"
  }, {
    "__config__": {
      "label": "滑块",
      "tag": "el-slider",
      "tagIcon": "slider",
      "defaultValue": 0,
      "span": 12,
      "showLabel": true,
      "layout": "colFormItem",
      "labelWidth": null,
      "required": true,
      "regList": [],
      "changeTag": true,
      "document": "https://element.eleme.cn/#/zh-CN/component/slider",
      "formId": 109,
      "renderKey": 1589018104973
    },
    "disabled": false,
    "min": 0,
    "max": 100,
    "step": 1,
    "show-stops": false,
    "range": false,
    "__vModel__": "field109"
  }],
  "formRef": "elForm",
  "formModel": "formData",
  "size": "medium",
  "labelPosition": "right",
  "labelWidth": 100,
  "formRules": "rules",
  "gutter": 15,
  "disabled": false,
  "span": 12,
  "formBtns": true
}
,
      formConf2: {
        fields: [
          {
            __config__: {
              label: '单行文本',
              labelWidth: null,
              showLabel: true,
              changeTag: true,
              tag: 'el-input',
              tagIcon: 'input',
              required: true,
              layout: 'colFormItem',
              span: 24,
              document: 'https://element.eleme.cn/#/zh-CN/component/input',
              regList: [
                {
                  pattern: '/^1(3|4|5|7|8|9)\\d{9}$/',
                  message: '手机号格式错误'
                }
              ]
            },
            __slot__: {
              prepend: '',
              append: ''
            },
            __vModel__: 'mobile',
            placeholder: '请输入手机号',
            style: {
              width: '100%'
            },
            clearable: true,
            'prefix-icon': 'el-icon-mobile',
            'suffix-icon': '',
            maxlength: 11,
            'show-word-limit': true,
            readonly: false,
            disabled: false
          },
          {
            __config__: {
              label: '日期范围',
              tag: 'el-date-picker',
              tagIcon: 'date-range',
              defaultValue: null,
              span: 24,
              showLabel: true,
              labelWidth: null,
              required: true,
              layout: 'colFormItem',
              regList: [],
              changeTag: true,
              document:
                'https://element.eleme.cn/#/zh-CN/component/date-picker',
              formId: 101,
              renderKey: 1585980082729
            },
            style: {
              width: '100%'
            },
            type: 'daterange',
            'range-separator': '至',
            'start-placeholder': '开始日期',
            'end-placeholder': '结束日期',
            disabled: false,
            clearable: true,
            format: 'yyyy-MM-dd',
            'value-format': 'yyyy-MM-dd',
            readonly: false,
            __vModel__: 'field101'
          }
        ],
        formRef: 'elForm',
        formModel: 'formData',
        size: 'small',
        labelPosition: 'right',
        labelWidth: 100,
        formRules: 'rules',
        gutter: 15,
        disabled: false,
        span: 24,
        formBtns: true,
        unFocusedComponentBorder: false
      }
    }
  },
  computed: {},
  watch: {},
  created() {},
  mounted() {},
  methods: {
    change() {
      this.key2 = +new Date()
      const t = this.formConf
      this.formConf = this.formConf2
      this.formConf2 = t
    },
    sumbitForm1(data) {
      console.log('sumbitForm1提交数据：', data)
    },
    sumbitForm2(data) {
      console.log('sumbitForm2提交数据：', data)
    }
  }
}
</script>

<style lang="scss" scoped>
.test-form {
  margin: 15px auto;
  width: 800px;
  padding: 15px;
}
</style>
