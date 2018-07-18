<template>
  <div>
    <div class="counter-wrap">
      <span class="minus" @click="minus">-</span>
      <input type="text" v-model="number" @keyup="fixNumber"/>
      <span class="add" @click="add">+</span>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        number: this.min,
      }
    },
    props: {
      min: {
        type: Number,
        default: 1
      },
      max: {
        type: Number,
        default: 10
      }
    },
    watch: {
      number() {
        this.$emit("on-change", this.number)
      }
    },
    methods: {
      fixNumber () {//有个bug，chorme在输入框中用中文输入法的时候，会出现非数字字符去不掉问题
        let fix
        console.log(this.number);
        if (typeof this.number === 'string') {
          fix = Number(this.number.replace(/\D/g, ''))
        }
        else {
          fix = this.number
        }
        if (fix > this.max || fix < this.min) {
          fix = this.min
        }
        this.number = fix
      },
      minus () {
        if (this.number <= this.min) {
          return this.min
        }
        return --this.number
      },
      add () {
        if (this.number >= this.max ) {
          return this.max
        }
        return ++this.number
      }
    }
  }
</script>

<style scoped>
  .counter-wrap {
    height: 30px;
    border: 1px solid #e3e3e3;
    border-radius: 3px;
    display: inline-block;
  }

  .minus{
    width: 20px;
    display: inline-block;
    text-align: center;
    height: 30px;
    line-height: 30px;
    border-right: 1px solid #e3e3e3;
    cursor: pointer;
  }

  .add {
    width: 20px;
    display: inline-block;
    text-align: center;
    height: 30px;
    line-height: 30px;
    border-left: 1px solid #e3e3e3;
    cursor: pointer;
  }

  .counter-wrap input{
    height: 19px;
    line-height: 19px;
    width: 30px;
    text-align: right;
    border: none;
    padding: 5px 10px;
  }
</style>
