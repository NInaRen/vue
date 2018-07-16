<template>
  <div class="sliderShow">
    <a :href="slides[nowIndex].href" @mouseout="runInv" @mouseover="clearInv">
      <img :src="slides[nowIndex].src"/>
    </a>
    <div class="pagination">
      <span>{{ slides[nowIndex].title }}</span>
      <div class="pages">
        <span @click="goToPage(prevIndex)"><</span>
        <span v-for="(item, index) in slides" @click="goToPage(index)" :class="{line:index === nowIndex}">{{ index + 1 }}</span>
        <span @click="goToPage(nextIndex)">></span>
      </div>
    </div>

  </div>
</template>

<script>
  export default {
    props: {
      slides: {
        type: Array,
        default: []
      },
      itvTime: {
        type: Number,
        default: 1000
      }
    },
    data () {
      return {
        nowIndex: 0,
      }
    },
    computed: {
      prevIndex() {
        if (this.nowIndex === 0) {
          return this.slides.length - 1;
        } else {
          return this.nowIndex - 1;
        }
      },
      nextIndex() {
        if (this.nowIndex === this.slides.length - 1) {
          return 0;
        } else {
          return this.nowIndex + 1;
        }
      }
    },
    methods: {
      goToPage(index) {
        this.nowIndex = index;
      },
      runInv() {
        this.invId = setInterval(() => {
          this.goToPage(this.nextIndex)
        }, this.itvTime);
      },
      clearInv() {
        clearInterval(this.invId);
      },
    },
    mounted () {
      this.runInv();
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .sliderShow {
    width: 100%;
    height: 400px;
  }
  .sliderShow img {
    width: 100%;
    height: 400px;
  }
  .pagination {
    background-color: #ccc;
    opacity: 0.5;
    height: 50px;
    line-height: 50px;
    width: 100%;
    z-index: 10;
    margin-top: -50px;
    padding: 0 20px;
    box-sizing: border-box;
  }
  .pages {
    float: right;
    right: 40px;
  }
  .pages span {
    padding: 5px;
  }
  .line {
    border-bottom: 1px solid red;
  }
</style>
