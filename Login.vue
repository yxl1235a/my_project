    <template>
    <div class="login">
  <el-card class="box-card">
  <div slot="header" class="clearfix">
    <span>后台管理商城系统</span>
  </div>
    <el-tabs 
    v-model="currentIndex"
     stretch @tab-click="handleTabsClick">
      <el-tab-pane 
      label="登录" 
      name="login">
         <el-form 
         :model="loginForm"
          status-icon 
          label-width="60px"
          ref="loginForm"
          :rules="rules">
      <el-form-item
       label="用户名"
        prop="username">
       <el-input 
       type="text"
       v-model="loginForm.username">
       </el-input> 
      </el-form-item>
        <el-form-item 
        label="密码"
        prop="password">
       <el-input 
       type="password"
       v-model="loginForm.password">
       </el-input>  
      </el-form-item>
      <el-form-item>
       <el-button 
       type="primary" 
       @click="submitForm('loginForm')"
       >登录</el-button>  
      </el-form-item>

  </el-form>
        </el-tab-pane>
      <el-tab-pane label="注册" name="register">
         <el-form 
         :model="registerForm" 
         status-icon label-width="60px" 
         ref="registerForm">
      <el-form-item 
      label="用户名"
       prop="username">
       <el-input
        type="text"
         v-model="registerForm.username">
         </el-input> 
      </el-form-item>
        <el-form-item 
        label="密码"
         prop="password">
       <el-input 
       type="password"
        v-model="registerForm.password">
        </el-input>  
      </el-form-item>
       <el-form-item 
        label="确认密码"
         prop="configurePassword">
       <el-input 
       type="password"
        v-model="registerForm.configurePassword">
        </el-input>  
      </el-form-item>
      <el-form-item>
       <el-button type="primary"
        @click="submitForm('registerForm')"
        >登录</el-button>  
      </el-form-item>
      </el-tab-pane>
    </el-tabs>
  </el-card>
    </div>
</template>

<script
>
export default {
  data() {
    // 验证规则
    var validateUserName = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入用户名"));
      } else if (value.length < 6) {
        callback(new Error("长度不够"));
      } else {
        callback();
      }
    };
    var validatePassWord = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入密码"));
      } else {
        callback();
      }
    };
    // 验证规则
    var validateUserName = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入用户名"));
      } else if (value.length < 6) {
        callback(new Error("长度不够"));
      } else {
        callback();
      }
    };
    var validatePassWord = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入密码"));
      } else {
        callback();
      }
    };
    var validateConfigPassword=(rule,value,callback)=>{
      if(value===''){
        callback(new Error("请输入密码"))
      }else if(value !== this.registerForm.Password){
        callback(new Error("两次密码不一致"))
      }else{
        callback();
      }
    }
    return {
      currentIndex: "login",
      loginForm: {
        username: "",
        password: "",
      },
      registerForm:{
        username:"",
        password:"",
        configurePassword:""
      },
      activeTab:"login",
      rules: {
        username: [
          {
            validator: validateUserName,
            trigger: "blur",
          },
        ],
        password: [
          {
            validator: validatePassWord,
            trigger: "blur",
          },
        ],
        configurePassword:[{
          validator:validateConfigPassword,trigger:"blur"
        }]
      },
    };
  },
  methods: {
    submitForm(forName) {
      this.$refs[forName].validate((valid) => {
        if (valid) {
          if(this.activeTab==="login"){
            console.log(this.loginForm);
          }
          if(this.activeTab==="register"){
            console.log(this.registerForm);
          }
            
        } else {
          return;
        }
      });
    },
    handleTabsClick(tab){
      this.activeTab=tab.name;
    }
  },
};
</script>

<style scoped>
.login {
  width: 1200px;
  margin: 0 auto;
}
.box-card {
  width: 500px;
  margin: 100px auto;
}
</style>