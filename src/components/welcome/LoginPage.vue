<template>
  <div style="text-align: center; margin: 0 40px">
    <div style="margin-top: 150px">
      <div style="font-size: 25px">登录</div>
      <div style="font-size: 14px;color: grey;margin-top: 10px">进入系统前请先登录</div>
    </div>
    <div style="margin-top: 40px">
      <el-input v-model="EmailLoginForm.email" :prefix-icon="User" type="text" placeholder="邮箱"/>
      <el-input v-model="EmailLoginForm.password" :prefix-icon="Lock" type="password" placeholder="密码" style="margin-top: 10px"/>
    </div>
    <el-row style="margin-top: 10px">
      <el-col :span="12" style="text-align: left">
        <el-checkbox v-model="EmailLoginForm.remember" label="记住我" size="large"/>
      </el-col>
      <el-col :span="12" style="text-align: right">
        <el-link>忘记密码？</el-link>
      </el-col>
    </el-row>
    <div style="margin-top: 50px">
      <el-button @click="EmailLogin()" style="width: 250px" type="success" plain>立即登录</el-button>
    </div>
    <el-divider>
      <span style="color: grey;font-size: 14px">没有账号</span>
    </el-divider>
    <div>
      <el-button style="width: 250px" type="warning" plain>注册账号</el-button>
    </div>
  </div>
</template>

<script setup>
import {User, Lock} from '@element-plus/icons-vue'
import {reactive} from "vue"
import {ElMessage} from "element-plus";
import router from "@/router";
import {post} from "@/assets/js";

const EmailLoginForm = reactive({
  email: '',
  password: '',
  remember: false
})

const EmailLogin = () => {
  if(!EmailLoginForm.email || !EmailLoginForm.password){
    ElMessage.warning("请输入邮箱和密码")
  }else {
    post("/login/emailLogin", {
      user:{
        email: EmailLoginForm.email,
        password: EmailLoginForm.password,
        remember: EmailLoginForm.remember
      },
    }, (message) => {
      ElMessage.success(message)
      router.push('/index')
    })
  }
}
</script>

<style scoped>

</style>