<template>
    <div class="login_container">
    <div class="login_box">
        <!-- 头像区域 -->
        <div class="avatar_box">
            <img src="../assets/logo.png" alt="">
        </div>
        <!-- 登录表单区域 -->
        <el-form ref="formRef" class="login_form" :model="form" :rules="formRules">
         <el-form-item prop="username">
            <el-input v-model="form.username" prefix-icon="el-icon-user-solid"></el-input>
         </el-form-item>
         <el-form-item prop="password">
            <el-input type="password" v-model="form.password" prefix-icon="el-icon-s-promotion"></el-input>
         </el-form-item>
         <el-form-item class="btns">
            <el-button type="primary" @click="login">登录</el-button>
            <el-button type="info" @click="resetForm">重置</el-button>
         </el-form-item>
        </el-form>
    </div>
    </div>
</template>

<script>
export default {
  data () {
    return {
      form: {
        username: 'yyy',
        password: '123456'
      },
      // 这是表单验证规则
      formRules: {
        // 用户名校验规则
        username: [
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 3, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur' }
        ],
        // 密码校验规则
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 15, message: '长度在 6 到 15 个字符', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    resetForm () {
      this.$refs.formRef.resetFields()
    },
    login () {
      this.$refs.formRef.validate((valid) => {
        if (!valid) alert('请注意用户名密码是否符合格式')
        var result = this.$http.post('login', this.form)
        console.log(result)
      })
    }
  }
}

</script>

<style lang="less" scoped>
.login_container{
    background-color: #2b4b6b;
    height: 100%;
}

.login_box{
    width: 450px;
    height: 300px;
    background-color: #fff;
    border-radius: 3px;
    position: absolute;
    left: 50%;
    top:50%;
    transform:translate(-50%,-50%);

    .avatar_box{
        width: 130px;
        height: 130px;
        border:1px solid #eee;
        border-radius: 50%;
        padding: 10px;
        box-shadow: 0 0 10px #ddd;
        position: absolute;
        left: 50%;
        transform: translate(-50%,-50%);
        background-color: #fff;
        img{
            width: 100%;
            height: 100%;
            border-radius: 50%;
            background-color: #eee;
        }
    }
}

.login_form{
    position: absolute;
    bottom: 0;
    width: 100%;
    padding: 0 20px;
    box-sizing: border-box;
}

.btns{
    display: flex;
    justify-content: flex-end;
}

</style>
