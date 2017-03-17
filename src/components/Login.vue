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
            <el-button type="primary" @click="loginToDo">登录</el-button>
          </el-form-item>
        </el-form>
        <span>测试账号：1，密码：1</span>
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
      created() {
        let account = localStorage.getItem('account');
        if(account){
          this.$router.push('/todolist');
        }
      },
      methods: {
        loginToDo() {
          if(this.account === '1'&&this.password === '1'){
           localStorage.setItem('account',this.account);
           this.$router.push('/todolist');
          }else{
            this.$message({
              type:'error',
              message:'账号密码错误！'
            });
          }
        }
      }
    };
</script>
