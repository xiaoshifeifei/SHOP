<template>
    <div class="logg">
        <div class="login_first">
            <!-- 登录头 -->
            <div class="login_log">
                <img src="../assets/logo.png" alt="">
            </div>
            <!-- 账号密码输入框 -->
            <div class="login_yan">
                <el-form :model="rulesForm" :rules="rulefo" ref="login_baybay" label-width="0px" class="demo-ruleForm">
                    <el-form-item prop="username">
                        <el-input v-model="rulesForm.username" prefix-icon="iconfont icon-user"></el-input>
                    </el-form-item>
                    <el-form-item prop="password">
                        <el-input v-model="rulesForm.password" type="password" prefix-icon="iconfont icon-3702mima">
                        </el-input>
                    </el-form-item>
                </el-form>
                <!-- 登录与注册 -->
                <div class="login_btn">
                    <el-row>
                        <el-button type="primary" @click="login_go">登录</el-button>
                        <el-button type="info" @click="login_bay">重置</el-button>
                    </el-row>
                </div>
            </div>

        </div>
    </div>
</template>
<script>
    import {
        login_api
    } from '@/api'
    export default {
        data() {
            return {
                // 登录数据双向绑定对象
                rulesForm: {
                    username: 'admin',
                    password: '123456',
                },
                // 验证规则
                rulefo: {
                    username: [{
                        required: true,
                        message: '请输入用户名',
                        trigger: 'blur'
                    }, {
                        min: 3,
                        max: 5,
                        message: '长度在 3 到 5 个字符',
                        trigger: 'blur'
                    }],
                    password: [{
                        required: true,
                        message: '请输入密码',
                        trigger: 'blur'
                    }, {
                        min: 3,
                        max: 10,
                        message: '长度在 3 到 10 个字符',
                        trigger: 'blur'
                    }]
                }
            }
        },
        methods: {
            login_go() {
                this.$refs.login_baybay.validate(async vali => {
                    if (!vali) return
                    const {
                        data: res
                    } = await login_api(this.rulesForm)
                    console.log(res, 111);
                    window.sessionStorage.setItem('token', res.data.token)
                    this.$router.push('/home')
                })

            },
            // 表单的重置功能 通过引用ref 得到实例，调用表单重置的方法
            //效果就是清楚了表单验证规则，然后重置到初始化状态，这就是表单的重置功能
            login_bay() {
                this.$refs.login_baybay.resetFields();
            }
        },
        created() {

        },

    }
</script>
<style lang="less" scoped>
    .logg {
        height: 100%;
        background-color: #2B4B6B;
    }
    
    .login_first {
        width: 450px;
        height: 300px;
        background-color: #fff;
        border-radius: 5px;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        .login_log {
            width: 150px;
            height: 150px;
            background-color: #fff;
            box-shadow: 0px 0px 28px -2px #E9EAEC;
            border-radius: 50%;
            position: absolute;
            left: 50%;
            transform: translate(-50%, -50%);
            img {
                width: 120px;
                border-radius: 50%;
                background-color: #EEEEEE;
                position: absolute;
                top: 16px;
                left: 15px;
            }
        }
    }
    
    .login_yan {
        margin-top: 100px;
        margin-left: 25px;
        width: 400px;
        .login_btn {
            padding-left: 250px;
        }
    }
</style>