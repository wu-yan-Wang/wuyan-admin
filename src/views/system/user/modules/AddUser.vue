<template>
  <a-modal
    title="新建人员"
    :width="800"
    :visible="visible"
    :confirmLoading="confirmLoading"
    @ok="handleSubmit"
    @cancel="handleCancel"
  >
    <a-spin :spinning="confirmLoading">
      <a-form :form="form" class="form">
        <a-row class="form-row" :gutter="16">
          <a-col v-bind="col3">
            <a-form-item
              label="账号"
            >
              <a-input v-decorator="['account', {rules: [{required: true, min: 6 ,max:18, message: '账号必须在6~18位！'}]}]" />
            </a-form-item>
          </a-col>
          <a-col v-bind="col3">
            <a-form-item
              label="姓名"
            >
              <a-input v-decorator="['name', {rules: [{required: true, max: 6, message: '姓名最多输入五个字符！'}]}]" />
            </a-form-item>
          </a-col>
          <a-col v-bind="col3">
            <a-form-item
              label="性别"
            >
              <dict-select
                :allowClear="true"
                placeholder="选择"
                v-decorator="['sex', {
                  initialValue:data.sex,
                  rules: [{required: true, message: '请选择性别！'}]
                }]"></dict-select>
            </a-form-item>
          </a-col>
          <a-col v-bind="col3">
            <a-form-item
              label="手机号"
            >
              <a-input
                v-decorator="['mobilePhone',{
                  rules: [{required: true, max: 11,pattern:$enum('form.rule.phone') ,message: '请输入正确的手机号！'}]
                }]" />
            </a-form-item>
          </a-col>
          <a-col v-bind="col3">
            <a-form-item label="email">
              <a-input
                v-decorator="['email',{
                  rules:[{type:'email',message:'请输入正确的邮箱！'}]
                }]"></a-input>
            </a-form-item>
          </a-col>
        </a-row>
      </a-form>
    </a-spin>
  </a-modal>
</template>

<script>
import DictSelect from '@/components/DictSelect'
export default {
  data () {
    return {
      visible: false,
      confirmLoading: false,
      form: this.$form.createForm(this),
      col3: this.$enum('form.col2'),
      data: {}
    }
  },
  created () {
  },
  methods: {
    add () {
      this.visible = true
    },
    handleSubmit () {
      this.form.validateFields((err, values) => {
        this.confirmLoading = true
        if (!err) {
          console.log('Received values of form: ', values)
          this.confirmLoading = true
          setTimeout(() => {
            this.confirmLoading = false
            this.$emit('ok')
            this.handleCancel()
          }, 1000)
        } else {
          this.confirmLoading = false
        }
      })
    },
    handleCancel () {
      this.visible = false
    }
  },
  components: {
    DictSelect
  }
}
</script>

<style>

</style>
