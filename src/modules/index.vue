<template>
  <div class="login">
    <!-- BEGIN LOGIN -->
    <animated-fade-in>
      <div class="content" v-if="contentShow">
        <!-- BEGIN LOGIN FORM -->
        <formbox-group klass="login-form" v-show="activeForm === 'login'">
          <h4 class="form-title">登录到账户</h4>
          <alert v-model="alertShow" state="danger" :content="alertMessage"></alert>
          <formbox>
            <textbox placeholder="用户名" icon="user" v-model="username" @keyup.enter="login"></textbox>
          </formbox>
          <formbox>
            <textbox type="password" placeholder="密码" icon="lock" v-model="password" @keyup.enter="login"></textbox>
          </formbox>
          <div class="form-actions">
            <checkbox outline klass="rememberme">记住我</checkbox>
            <btn color="green" klass="pull-right" @click="login">登录</btn>
          </div>
        </formbox-group>
        <!-- END LOGIN FORM -->
      </div>
    </animated-fade-in>
    <!-- END LOGIN -->
    <canvas id="background"></canvas>
  </div>
</template>
<script>
  import router from '../router'
  import {Stage} from '@/untils'

  export default{
    data () {
      return {
        contentShow: false,
        activeForm: 'login',
        alertShow: false,
        alertMessage: '',
        username: 'admin',
        password: 'admin'
//        country: null
      }
    },
    methods: {
      login () {
        var self = this
        const username = this.username.trim()
        const password = this.password.trim()
        if (username === '' && password === '') {
          self.alertMessage = '请输入用户名和密码'
          this.alertShow = true
        } else {
          router.push('/main')
//          this.$store.dispatch('permission/login', {
//            username,
//            password
//          }).done(function (rst) {
//            router.push('/main')
//          }).fail(function (rst) {
//            self.alertMessage = rst.message
//            self.alertShow = true
//          })
        }
      },
//      handleCountryFlag (value) {
//        return require('../../static/img/global/flags/' + value.toLowerCase() + '.png')
//      },
      handleBackground () {
        var canvas = document.getElementById('background')
        canvas.width = window.innerWidth
        canvas.height = window.innerHeight
        var stage = new Stage(canvas, state => {
          if (state === 'second') {
            this.contentShow = true
          } else {
            this.contentShow = false
          }
        })
        stage.init()
        stage.loop()
      }
    },
    mounted () {
      this.handleBackground()
    }
  }
</script>
<style lang='sass'>
  @import "../assets/sass/style"
</style>
<style scoped>
  #background{
    position: absolute;
    top:0px;
    left: 0px;
    z-index: -1;
    background-color: #364150;
  }

  .login {
    background-color: transparent !important; }

  .login .logo {
    margin: 60px auto 20px auto;
    padding: 15px;
    text-align: center; }

  .login .content {
    background-color: #fff;
    width: 360px;
    margin: 0 auto;
    margin-top: 160px;
    margin-bottom: 0px;
    padding: 30px;
    padding-top: 20px;
    padding-bottom: 15px;
    -webkit-border-radius: 7px;
    -moz-border-radius: 7px;
    -ms-border-radius: 7px;
    -o-border-radius: 7px;
    border-radius: 7px; }

  .login .content h3 {
    color: #000; }

  .login .content h4 {
    color: #555; }

  .login .content p {
    color: #222; }

  .login .content .login-form,
  .login .content .forget-form {
    padding: 0px;
    margin: 0px; }

  .login .content .login-form .form-body,
  .login .content .forget-form .form-body,
  .login .content .register-form .form-body{
    padding: 0px !important; }

  .login .content .input-icon {
    border-left: 2px solid #44B6AE !important; }

  .login .content .input-icon {
    -webkit-border-radius: 4px;
    -moz-border-radius: 4px;
    -ms-border-radius: 4px;
    -o-border-radius: 4px;
    border-radius: 4px; }
  .login .content .input-icon .form-control {
    border-left: 0; }

  .login .content .form-title {
    font-weight: 300;
    margin-bottom: 25px; }

  .login .content .form-actions {
    background-color: #fff;
    clear: both;
    border: 0px;
    border-bottom: 1px solid #eee;
    padding: 0px 30px 25px 30px;
    margin-left: -30px;
    margin-right: -30px; }

  .login .content .forget-form .form-actions {
    border: 0;
    margin-bottom: 0;
    padding-bottom: 20px; }

  .login .content .register-form .form-actions {
    border: 0;
    margin-bottom: 0;
    padding-bottom: 0px; }

  .login .content .form-actions .rememberme {
    margin-top: 8px;
    display: inline-block; }

  .login .content .form-actions .btn {
    margin-top: 1px; }

  .login .content .forget-password {
    margin-top: 25px; }

  .login .content .create-account {
    border-top: 1px dotted #eee;
    padding-top: 10px;
    margin-top: 15px; }

  .login .content .create-account a {
    display: inline-block;
    margin-top: 5px; }

  /* multiselect */
  .login .content .multiselect__content-wrapper{
    z-index: 5;
  }

  .login .content .multiselect__input,
  .login .content .multiselect__single {
    padding: 1px 0 0 24px;
  }

  .login .content .multiselect__option .option__image{
    float: left;
    padding-top: 2px;
    padding-right: 8px;
  }

  /* footer copyright */
  .login .copyright {
    text-align: center;
    margin: 0 auto;
    padding: 10px;
    color: #999;
    font-size: 13px; }

  @media (max-width: 480px) {
    /***
    Login page
    ***/
    .login .logo {
      margin-top: 10px;
    }

    .login .content {
      width: 280px;
    }

    .login .content h3 {
      font-size: 22px;
    }

    .login .checkbox {
      font-size: 13px;
    }
  }
</style>
