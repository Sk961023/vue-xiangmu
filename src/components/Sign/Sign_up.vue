<template>
<div>
    <el-row :gutter="16">
        <el-col :span="12"><div class="grid-content bg-purple"><img class="signimg" src="../Img/sign.jpg" alt=""></div></el-col>
        <el-col :span="7" class="login">
            <div class="grid-content bg-purple">
                <el-form :model="ruleForm2" status-icon :rules="rules2" ref="ruleForm2" label-width="100px" class="demo-ruleForm">
                    <el-form-item label="用户名" prop="age">
                        <el-input v-model.number="ruleForm2.age"></el-input>
                    </el-form-item>
                    <el-form-item label="密码" prop="pass">
                        <el-input type="password" v-model="ruleForm2.pass" auto-complete="off"></el-input>
                    </el-form-item>
                    <el-form-item label="确认密码" prop="checkPass">
                        <el-input type="password" v-model="ruleForm2.checkPass" auto-complete="off"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button type="primary" class="button" @click="submitForm('ruleForm2')">注册</el-button>
                        <el-button class="button1" @click="resetForm('ruleForm2')">重置</el-button>
                    </el-form-item>
                </el-form>
            </div>
        </el-col>
        <el-col :span="5"><div class="grid-content bg-purple"></div></el-col>
    </el-row>
</div>
</template>

<script>
  export default {
    data() {
        var checkAge = (rule, value, callback) => {
            if (!value) {
            return callback(new Error('用户名不能为空'));
            }
            setTimeout(() => {
            if (!Number.isInteger(value)) {
                callback(new Error('请输入正确的用户名'));
            } else {
                // if (value < 18) {
                // callback(new Error('必须年满18岁'));
                // } else {
                callback();
                // }
            }
            }, 500);
        };
        var validatePass = (rule, value, callback) => {
            if (value === '') {
            callback(new Error('请输入密码'));
            } else {
            if (this.ruleForm2.checkPass !== '') {
                this.$refs.ruleForm2.validateField('checkPass');
            }
            callback();
            }
        };
        var validatePass2 = (rule, value, callback) => {
            if (value === '') {
            callback(new Error('请再次输入密码'));
            } else if (value !== this.ruleForm2.pass) {
            callback(new Error('两次输入密码不一致!'));
            } else {
            callback();
            }
        };
      return {
        ruleForm2: {
          pass: '',
          checkPass: '',
          age: ''
        },
        rules2: {
          pass: [
            { validator: validatePass, trigger: 'blur' }
          ],
          age: [
            { validator: checkAge, trigger: 'blur' }
          ],
           checkPass: [
            { validator: validatePass2, trigger: 'blur' }
          ],
        }
      };
    },
    methods: {
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            alert('submit!');
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.login{
    margin-top: 14%;
}
.button{
    width: 100%;
}
.button1{
    margin-top: 20px;
    width: 100%;
    margin-left: 0;
}
.signimg{
  margin-top:20%;
  margin-left: 17%;
}
</style>
