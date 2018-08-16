<template>
  <div>
    <div class="form-table">
      <div class="form-row">
        <div class="form-cell form-label">用户名：</div>
        <div class="form-cell form-input">
          <input v-model="usernameModel" type="text" placeholder="请输入用户名"/>
        </div>
        <div class="form-cell tip-message">{{ validateUserName.errorText }}</div>
      </div>
      <div class="form-row">
        <div class="form-cell form-label">密码:</div>
        <div class="form-cell form-input">
          <input v-model="passwordModel" type="password" placeholder="请输入密码"/>
        </div>
        <div class="form-cell tip-message">{{ validatePassword.errorText }}</div>
      </div>
      <div class="form-row">
        <div class="form-cell form-label"></div>
        <div class="form-cell form-input">
          <div class="login" @click="login">登录</div>
          <p class="error-text">{{errorText}}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        usernameModel: '',
        passwordModel: '',
        errorText: ''
      }
    },
    computed: {
      validateUserName() {
        let errorText,status
        if (!/@/g.test(this.usernameModel)) {
          status = false
          errorText = "登录名未包含@"
        }
        else {
          status = true
          errorText = ""
        }
        //首次进入不验证用户名
        if (!this.userFlag) {
          errorText = ''
          this.userFlag = true
        }
        return {
          status,
          errorText
        }
      },
      validatePassword() {
        let errorText,status
        if (!/^\w{1,6}$/g.test(this.passwordModel)) {
          status = false
          errorText = "密码不是1-6位"
        }
        else {
          status = true
          errorText = ""
        }
        //首次进入不验证密码
        if (!this.passwordFlag) {
          errorText = ''
          this.passwordFlag = true
        }
        return {
          status,
          errorText
        }
      },
    },
    methods: {
      login() {
        if (!this.validateUserName.status || !this.validatePassword.status) {
          this.errorText = '部分选项未通过'
        }
        else {
          this.errorText = ''
          this.$http.get('api/login')
            .then((res) => {
              this.$emit('has-log', res.data)
            }, (error) => {
              console.log(error)
            })
        }
      },
    }

  }

</script>
