<template>
  <div class="login">
    <el-row class="content">
      <el-col :xs="24" :sm="{span: 6,offset: 9}">
        <h2 class="title">欢迎登录</h2>
        <el-form ref="form" :model="form" >
          <el-form-item label="账号">
            <el-input v-model="account" placeholder="点击输入账号"></el-input>
          </el-form-item>
          <el-form-item label="密码">
            <el-input v-model="password" placeholder="点击输入密码"></el-input>
          </el-form-item>
          <el-form-item :span="12">
            <el-button type="primary" @click="onSubmit">登录</el-button>
          </el-form-item>
        </el-form>
      </el-col>
    </el-row>
  </div>
</template>
<style lang="stylus" scoped>
</style>
<script>
    export default{
      data() {
        return {
          account: '',
          password: ''
        };
      },
      methods: {
        onSubmit() {
           console.log(1);
        }
      }
    };
</script>
