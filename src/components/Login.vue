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
    import http from '@/http.js'
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
                        let param = {'account': this.formInline.account, 'password': this.formInline.password};
                        http.fetchGet("http://127.0.0.1:8081/user/login", param).then(response => {
                            if(response.data.response === 'Success') {
                                this.$router.push({path: '/welcome'})
                            } else {
                                alert('Error!');
                            }
                        })
                    } else {
                        this.$Message.error('表单校验失败');
                    }
                })
            }
        }
    }
</script>
