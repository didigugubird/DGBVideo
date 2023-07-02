<template>
  <div>
    欢迎进入
  </div>
  <div>
    <el-button type="danger">
      退出登录
    </el-button>
  </div>
</template>

<script setup>
const logout = () => {
  get('/api/auth/logout')
}
</script>

<style scoped>

</style>