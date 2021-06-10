    <template>
    <div class="login">
  <el-card class="box-card">
  <div slot="header" class="clearfix">
    <span>后台管理商城系统</span>
  </div>
    <el-tabs v-model="currentIndex" stretch>
      <el-tab-pane label="登录" name="login">
        登录
        <el-form :model="loginForm" status-icon label-width="60px" ref="loginForm" :rules="rules">
      <el-form-item label="用户名" prop="username">
       <el-input type="text" v-model="loginForm.username"></el-input> 
      </el-form-item>
        <el-form-item label="密码" prop="password">
       <el-input type="password" v-model="loginForm.password"></el-input>  
      </el-form-item>
      <el-form-item>
       <el-button type="primary" @click="submitForm('loginForm')">登录</el-button>  
      </el-form-item>
  </el-form>
        </el-tab-pane>
      <el-tab-pane label="注册" name="register">注册</el-tab-pane>
    </el-tabs>
  </el-card>
    </div>
</template>

<script
>
export default {
 
 data() {
     // 验证规则
    var validateUserName = (rule,value,callback)=>{
      if(value===''){
        callback(new Error('请输入用户名'))
      }else if(value.length <6){
        callback(new Error('长度不够'));
      }else{
        callback();
      }
    }
    var validatePassWord=(rule,value,callback)=>{
      if(value===''){
        callback(new Error("请输入密码"))
      }else{
        callback();
      }
    }
      return{
        currentIndex:"login",
        loginForm:{
          username:"",
          password:""
        },
        rules:{
          username:[
            {
              validator:validateUserName,trigger:"blur"
            }
          ],
          password:[{
            validator:validatePassWord,trigger:"blur"
          }]
        }
  } 
 },
 methods:{
   submitForm(forName){
     this.$refs[forName].validate((valid)=>{
       if(valid){
         console.log(this.loginForm);
       }else{
         return;
       }
     })
   }
 }
}
</script>

<style scoped>
  .login{
    width: 1200px;
    margin: 0 auto;
  }
  .box-card{
    width: 500px;
    margin: 100px auto;
  }
</style>