<style lang="less">
    @import './login.less';
</style>

<template>
    <div class="login" @keydown.enter="handleSubmit">
        <div class="login-con">
             <el-form class="form-con" ref="loginForm" :model="form" :rules="rules" label-width="60px">
                <el-form-item >
                    <p class="apptitle">{{apptitle}}</p>
                </el-form-item>
                <el-form-item label="用户名">
                   <el-input prop="userName" v-model="form.userName" placeholder="请输入用户名"/>
                </el-form-item>
                <el-form-item label="密码" >
                    <el-input prop="password" type="password" v-model="form.password" placeholder="请输入密码"/>
                </el-form-item>      
                <el-form-item class="login-con-click">
                    <p class="wrapper">
                        <el-button @click="gofundraising" type="primary">登录</el-button>
                        <el-button @click="goregister" type="primary">注册</el-button>
                    </p>
                </el-form-item>
            </el-form>       
        </div>
    </div>
</template>

<script>
import Cookies from 'js-cookie';
import fundraisingVue from '../fundraising/fundraising.vue';

export default {
    data () {
        return {
            form: {
                userName: '',
                password: ''
            },
            apptitle: this.$store.state.appname,
            rules: {
                userName: [
                    { required: true, message: '账号不能为空', trigger: 'blur' }
                ],
                password: [
                    { required: true, message: '密码不能为空', trigger: 'blur' }
                ]
            }
        };
    },
    methods: {
        gofundraising () {
            this.$router.push({path: 'fundraising'});
        },
        goregister () {
            this.$router.push({path: 'register'});
        },
        handleSubmit () {
          /*
            this.$refs.loginForm.validate((valid) => {
                if (valid) {
                    Cookies.set('user', this.form.userName);
                    Cookies.set('password', this.form.password);
                    this.$store.commit('setAvator', '../../assets/avator.png');
                    Cookies.set('access', 1);
                }
            });
            */
            
            this.$router.push({path: 'fundraising'});
        },
    }
};
</script>