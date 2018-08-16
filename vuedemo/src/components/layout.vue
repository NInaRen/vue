<template>
  <div>
    <div class="app-head">
      <div class="app-head-inner">
        <router-link :to="{ path:'/'}">
          <img src="../assets/logo.png"/>
        </router-link>

        <div class="head-nav">
          <ul class="nav-list">
            <li>{{username}}</li>
            <li v-if="username === ''" @click="logClick">登录</li>
            <li class="nav-pile">|</li>
            <li v-if="username === ''" @click="regClick">注册</li>
            <li v-if="username != ''" @click="quit">退出</li>
            <li class="nav-pile">|</li>
            <li @click="aboutClick">关于</li>
          </ul>
        </div>
      </div>

    </div>
    <div class="app-content">
      <keep-alive>
        <router-view></router-view>
      </keep-alive>
    </div>
    <div class="app-foot">
      <p> 2018 Learn Demo By NinaRen</p>
    </div>
    <my-dialog :isShow="isShowLogDialog" @on-close="closeDialog">
      <log-form @has-log="onSuccessLog"></log-form>
    </my-dialog>
    <my-dialog :isShow="isShowRegDialog" @on-close="closeDialog">
      <reg-form></reg-form>
    </my-dialog>
    <my-dialog :isShow="isShowAboutDialog" @on-close="closeDialog">
      <p>test</p>
    </my-dialog>
  </div>
</template>

<script>
  import Dialog from './dialog'
  import logForm from './logForm'
  import regForm from './regForm'
  export default {
    components: {
      MyDialog: Dialog,
      regForm,
      logForm
    },
    data () {
      return {
        isShowAboutDialog: false,
        isShowLogDialog: false,
        isShowRegDialog: false,
        username: ''
      }
    },
    methods: {
     logClick () {
        this.isShowLogDialog = true
      },
      regClick () {
        this.isShowRegDialog = true
      },
      aboutClick () {
        this.isShowAboutDialog = true
      },
      closeDialog() {
        this.isShowAboutDialog = false
        this.isShowLogDialog = false
        this.isShowRegDialog = false
      },
      onSuccessLog(data) {
        this.closeDialog()
        this.username = data.data.username
      },
      quit() {
        this.username = ''
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  html, body, div, span, applet, object, iframe,
  h1, h2, h3, h4, h5, h6, p, blockquote, pre,
  a, abbr, acronym, address, big, cite, code,
  del, dfn, em, img, ins, kbd, q, s, samp,
  small, strike, strong, sub, sup, tt, var,
  b, u, i, center,
  dl, dt, dd, ol, ul, li,
  fieldset, form, label, legend,
  table, caption, tbody, tfoot, thead, tr, th, td,
  article, aside, canvas, details, embed,
  figure, figcaption, footer, header, hgroup,
  menu, nav, output, ruby, section, summary,
  time, mark, audio, video {
    margin: 0;
    padding: 0;
    border: 0;
    font-size: 100%;
    font: inherit;
    vertical-align: baseline;
  }
  /* HTML5 display-role reset for older browsers */
  article, aside, details, figcaption, figure,
  footer, header, hgroup, menu, nav, section {
    display: block;
  }
  body {
    line-height: 1;
  }
  ol, ul {
    list-style: none;
  }
  blockquote, q {
    quotes: none;
  }
  blockquote:before, blockquote:after,
  q:before, q:after {
    content: '';
    content: none;
  }
  table {
    border-collapse: collapse;
    border-spacing: 0;
  }
  a {
    color: inherit;
    text-decoration: none;
  }
  body {
    background: #f0f2f5;
    font-family: "Helvetica Neue",Helvetica,Arial,"Hiragino Sans GB","Hiragino Sans GB W3","Microsoft YaHei UI","Microsoft YaHei","WenQuanYi Micro Hei",sans-serif;
    font-size: 14px;
    color: #444;
  }
  .app-head {
    background: #363636;
    color: #b2b2b2;
    height: 70px;
    line-height: 70px;
    width: 100%;
  }
  .app-head-inner {
    width: 1200px;
    margin: 0 auto;
  }
  .app-head-inner img {
    width: 40px;
    margin-top: 15px;
  }
  .head-nav {
    float: right;
  }
  .nav-list {
    list-style: none;
    margin: 0;
  }
  .nav-list li{
    float: left;
    cursor: pointer;
  }
  .nav-pile {
    padding: 0 5px;
  }
  .app-foot {
    height: 70px;
    background: #EEEEEE;
    line-height: 70px;
    text-align: center;
    font-size: 15px;
    color: #666666;
    float: left;
    width: 100%;
  }
  .app-content {
    width: 1200px;
    margin: 0 auto;
  }

  .form-table {
    display: table;
    width:90%;
    margin: 15px auto;
  }

  .form-row {
    display: table-row;
  }

  .form-cell {
    display: table-cell;
    height: 45px;
    line-height: 45px;
  }

  .form-label {
    width: 120px;
    text-align: right;
    padding-right: 10px;
  }

  .form-input {
    width: calc(60% - 60px);
    min-width: 120px;
  }

  .tip-message {
    width: calc(40% - 60px);
    min-width: 120px;
  }

  .form-input input{
    border: 1px solid #999;
    border-radius: 4px;
    height: 30px;
    line-height: 30px;
    font-size: 16px;
    min-width: 90px;
    width: 100%;
    padding-left: 10px;
    box-sizing: border-box;
  }

  .login {
    text-align: center;
    width: 100%;
    line-height: 35px;
    height: 35px;
    color: white;
    font-size: 17px;
    background-color: #31c1a6;
    border-radius: 4px;
    cursor: pointer;
    margin-top: 15px;
  }

  .tip-message {
    padding-left: 15px;
    font-size: 14px;
    color: red;
  }

  .error-text {
    text-align: center;
    font-size: 14px;
    color: red;
  }

</style>
