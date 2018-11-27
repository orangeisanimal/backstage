<template>
  <div class="login-wrap">
    <el-form label-position="top" label-width="80px" :model="formdata" class="login-form">
        <h2>用户登陆</h2>
      <el-form-item label="用户名">
        <el-input v-model="formdata.username"></el-input>
      </el-form-item>
      <el-form-item label="密码">
        <el-input v-model="formdata.password"></el-input>
      </el-form-item>
        <el-button type="success" plain class="login-btn" @click="UserList()">登陆</el-button>
    </el-form>
  </div>
</template>

<script>
export default {
  data(){
      return{
          formdata:{
              username:'',
              password:'',
          }
      }
  },
   methods:{
       //优化代码， 对性能不产生影响，只是美观,ES7语法
      async UserList(){
         const res = await this.$http.post('login',this.formdata)
          
           const {meta:{status,msg},data}=res.data
           if(status===200){
               //保存token
               const token =localStorage.setItem('token',data.token)
               this.$router.push({name:'home'})
               this.$message.success(msg);
           }else{
               this.$message.warning(msg)
           }
           
       }
   }
}
</script>

<style>
.login-wrap{
    height: 100%;
    background-color:#324152;
    display: flex;
    justify-content: center;
    align-items: center;
}
.login-wrap .login-form{
   width: 400px;
   background-color:#fff;
   border-radius: 15px;
   padding: 30px;
}
.login-wrap .login-btn{
        width:100%;
        background-color: skyblue;
}
</style>
