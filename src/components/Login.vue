<template>
  <Form ref="formInline" :model="formInline" :rules="ruleInline" inline>
    <FormItem prop="account">
      <Input type="text" v-model="formInline.account" placeholder="用户名">
      <Icon type="ios-person-outline" slot="prepend"></Icon>
      </Input>
    </FormItem>
    <FormItem prop="password">
      <Input type="password" v-model="formInline.password" placeholder="密码">
      <Icon type="ios-lock-outline" slot="prepend"></Icon>
      </Input>
    </FormItem>
    <br /><br />
    <FormItem>
      <Button type="primary" @click="handleSubmit('formInline')">Signin</Button>
    </FormItem>
  </Form>
</template>
<script>
    import https from '@/http.js'
    export default {
        data () {
            return {
                formInline: {
                    account: '',
                    password: ''
                },
                ruleInline: {
                    account: [
                        { required: true, message: 'Please fill in the account', trigger: 'blur' }
                    ],
                    password: [
                        { required: true, message: 'Please fill in the password.', trigger: 'blur' },
                        { type: 'string', min: 6, message: 'The password length cannot be less than 6 bits', trigger: 'blur' }
                    ]
                }
            }
        },
        methods: {
            handleSubmit(name) {
                this.$refs[name].validate((valid) => {
                    if (valid) {
                        console.info('参数信息：', this.formInline);
                        let params = {'account': this.formInline.account, 'password': this.formInline.password};
                        https.fetchGet('/user/login', params).then(res => {

                            console.info('后台返回的数据：', res.data);
                        }).catch(err => {
                            console.info('报错信息：', err.response.message);
                        })
                    } else {
                        this.$Message.error('表单校验失败');
                    }
                })
            }
        }
    }
</script>
