<template>
  <a-modal
    :title="title"
    :width="width"
    :visible="visible"
    :confirmLoading="confirmLoading"
    @ok="handleOk"
    @cancel="handleCancel"
    cancelText="关闭">
    <a-spin :spinning="confirmLoading">
      <a-form :form="form">

        <a-form-item label="试题题目" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <a-input v-decorator="[ 'qtName', validatorRules.qtName]" placeholder="请输入试题题目"></a-input>
        </a-form-item>
        <a-form-item label="题目分数" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <a-input v-decorator="[ 'qtScore', validatorRules.qtScore]" placeholder="请输入题目分数"></a-input>
        </a-form-item>
        <a-form-item label="外键引自DIRECTION" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <j-dict-select-tag type="list" v-decorator="['dirId', validatorRules.dirId]" :trigger-change="true" dictCode="etc_exa_dir" placeholder="请选择外键引自DIRECTION"/>
        </a-form-item>
        <a-form-item label="试题难度,分别是:1 简单,2 中等,3 困难" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <a-input v-decorator="[ 'diff', validatorRules.diff]" placeholder="请输入试题难度,分别是:1 简单,2 中等,3 困难"></a-input>
        </a-form-item>
        <a-form-item label="引用自QT_TYPE" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <j-dict-select-tag type="list" v-decorator="['typeId', validatorRules.typeId]" :trigger-change="true" dictCode="etc_exa_type" placeholder="请选择引用自QT_TYPE"/>
        </a-form-item>
        <a-form-item label="引自SUBJECT" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <j-dict-select-tag type="list" v-decorator="['subId', validatorRules.subId]" :trigger-change="true" dictCode="etc_exa_sub" placeholder="请选择引自SUBJECT"/>
        </a-form-item>
        <a-form-item label="选项A" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <a-input v-decorator="[ 'opta', validatorRules.opta]" placeholder="请输入选项A"></a-input>
        </a-form-item>
        <a-form-item label="选项B" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <a-input v-decorator="[ 'optb', validatorRules.optb]" placeholder="请输入选项B"></a-input>
        </a-form-item>
        <a-form-item label="选项C" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <a-input v-decorator="[ 'optc', validatorRules.optc]" placeholder="请输入选项C"></a-input>
        </a-form-item>
        <a-form-item label="选项D" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <a-input v-decorator="[ 'optd', validatorRules.optd]" placeholder="请输入选项D"></a-input>
        </a-form-item>
        <a-form-item label="选项E" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <a-input v-decorator="[ 'opte', validatorRules.opte]" placeholder="请输入选项E"></a-input>
        </a-form-item>
        <a-form-item label="选项F" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <a-input v-decorator="[ 'optf', validatorRules.optf]" placeholder="请输入选项F"></a-input>
        </a-form-item>
        <a-form-item label="选项G" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <a-input v-decorator="[ 'optg', validatorRules.optg]" placeholder="请输入选项G"></a-input>
        </a-form-item>
        <a-form-item label="答案" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <a-input v-decorator="[ 'answer', validatorRules.answer]" placeholder="请输入答案"></a-input>
        </a-form-item>
        <a-form-item label="标记,表示当前试题是否被选中" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <a-input v-decorator="[ 'mark', validatorRules.mark]" placeholder="请输入标记,表示当前试题是否被选中"></a-input>
        </a-form-item>
        <a-form-item label="创建时间" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <j-date placeholder="请选择创建时间" v-decorator="[ 'createTime', validatorRules.createTime]" :trigger-change="true" style="width: 100%"/>
        </a-form-item>

      </a-form>
    </a-spin>
  </a-modal>
</template>

<script>

  import { httpAction } from '@/api/manage'
  import pick from 'lodash.pick'
  import { validateDuplicateValue } from '@/utils/util'
  import JDate from '@/components/jeecg/JDate'  
  import JDictSelectTag from "@/components/dict/JDictSelectTag"

  export default {
    name: "EtcQuestionModal",
    components: { 
      JDate,
      JDictSelectTag,
    },
    data () {
      return {
        form: this.$form.createForm(this),
        title:"操作",
        width:800,
        visible: false,
        model: {},
        labelCol: {
          xs: { span: 24 },
          sm: { span: 5 },
        },
        wrapperCol: {
          xs: { span: 24 },
          sm: { span: 16 },
        },
        confirmLoading: false,
        validatorRules: {
          qtName: {rules: [
          ]},
          qtScore: {rules: [
          ]},
          dirId: {rules: [
          ]},
          diff: {rules: [
          ]},
          typeId: {rules: [
          ]},
          subId: {rules: [
          ]},
          opta: {rules: [
          ]},
          optb: {rules: [
          ]},
          optc: {rules: [
          ]},
          optd: {rules: [
          ]},
          opte: {rules: [
          ]},
          optf: {rules: [
          ]},
          optg: {rules: [
          ]},
          answer: {rules: [
          ]},
          mark: {rules: [
          ]},
          createTime: {rules: [
          ]},
        },
        url: {
          add: "/exam/etcQuestion/add",
          edit: "/exam/etcQuestion/edit",
        }
      }
    },
    created () {
    },
    methods: {
      add () {
        this.edit({});
      },
      edit (record) {
        this.form.resetFields();
        this.model = Object.assign({}, record);
        this.visible = true;
        this.$nextTick(() => {
          this.form.setFieldsValue(pick(this.model,'qtName','qtScore','dirId','diff','typeId','subId','opta','optb','optc','optd','opte','optf','optg','answer','mark','createTime'))
        })
      },
      close () {
        this.$emit('close');
        this.visible = false;
      },
      handleOk () {
        const that = this;
        // 触发表单验证
        this.form.validateFields((err, values) => {
          if (!err) {
            that.confirmLoading = true;
            let httpurl = '';
            let method = '';
            if(!this.model.id){
              httpurl+=this.url.add;
              method = 'post';
            }else{
              httpurl+=this.url.edit;
               method = 'put';
            }
            let formData = Object.assign(this.model, values);
            console.log("表单提交数据",formData)
            httpAction(httpurl,formData,method).then((res)=>{
              if(res.success){
                that.$message.success(res.message);
                that.$emit('ok');
              }else{
                that.$message.warning(res.message);
              }
            }).finally(() => {
              that.confirmLoading = false;
              that.close();
            })
          }
         
        })
      },
      handleCancel () {
        this.close()
      },
      popupCallback(row){
        this.form.setFieldsValue(pick(row,'qtName','qtScore','dirId','diff','typeId','subId','opta','optb','optc','optd','opte','optf','optg','answer','mark','createTime'))
      },

      
    }
  }
</script>