<template>
  <div>
    <div class="chooser-wrap">
      <span v-for="(item, index) in chooseTypes"
            @click="chooseType(index)"
            :class="{active:index === nowIndex}">
        {{ item.label }}
      </span>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      chooseTypes: {
        type: Array,
        default: [
          {
            label: "123",
            value: 123
          }
        ]
      }
    },
    data() {
      return {
        nowIndex: 0
      }
    },
    methods: {
      chooseType(index) {
        this.nowIndex = index
        this.$emit("on-change", this.chooseTypes[this.nowIndex])
      }
    }
  }
</script>

<style scoped>
  .chooser-wrap {
    width: 100%;
  }

  .chooser-wrap span {
    padding: 7px 10px;
    border: 1px solid #e3e3e3;
    border-radius: 3px;
    margin: 0px 10px 0px 0;
    background: #fff;
    cursor: pointer;
    display: inline-block;
  }

  .chooser-wrap .active {
    border-color: #4fc08d;
    background: #4fc08d;
    color: #fff;
  }
</style>
