<template>
  <div>
    <div class="order-wrap">
      <div class="search-wrap">
        <div class="selection">
          选择产品：
          <v-selection :selections="products" @on-change="onParamChange"></v-selection>
        </div>
        <div class="selection">
          开始日期：
          <datepicker :date="startDate" :option="option"  @change="getTableData"></datepicker>
        </div>
        <div class="selection">
          结束日期：
          <datepicker :date="endDate" :option="option" @change="getTableData"></datepicker>
        </div>
        <div class="selection">
          关键词：
          <input class="keyword" v-model.lazy="keyword" type="text"/>
        </div>
      </div>
      <div>
        <table class="order-list">
          <tr>
            <th v-for="item in tableHeads">{{item.label}}</th>
          </tr>
          <tr v-for="item in tableData" :key="item.period">
            <td v-for="head in tableHeads">{{item[head.key]}}</td>
          </tr>
        </table>
      </div>
    </div>
  </div>

</template>

<script>
  import VSelection from '../components/selection.vue'
  import Datepicker from 'vue-datepicker/vue-datepicker-es6.vue'
  export default {
    components: {
      VSelection,
      Datepicker
    },
    data() {
      return {
        startDate: {
          time: ''
        },
        endDate: {
          time: ''
        },
        keyword:'',
        productTye: '0',
        products: [
          {
            label: '数据统计',
            value: 0
          },
          {
            label: '数据预测',
            value: 1
          },
          {
            label: '流量分析',
            value: 2
          },
          {
            label: '广告发布',
            value: 3
          }
        ],
        tableHeads: [
          {
            label: '订单号',
            key: 'orderId'
          },
          {
            label: '购买产品',
            key: 'product'
          },
          {
            label: '版本类型',
            key: 'version'
          },
          {
            label: '有效时间',
            key: 'period'
          },
          {
            label: '购买日期',
            key: 'date'
          },
          {
            label: '数量',
            key: 'buyNum'
          },
          {
            label: '总价',
            key: 'amount'
          }
        ],
        currentOrder: 'asc',
        tableData: [],
        option: {
          type: 'day',
          week: ['一', '二', '三', '四', '五', '六', '日'],
          month: ['1月', '2月', '3月', '4月', '5月', '6月', '7月', '8月', '9月', '10月', '11月', '12月'],
          format: 'YYYY-MM-DD',
          inputStyle: {
            'display': 'inline-block',
            'padding': '5px',
            'line-height': '15px',
            'font-size': '14px',
            'border': '2px solid #fff',
            'border-radius': '2px',
            'color': '#5F5F5F'
          },
          color: {
            header: '#ccc',
            headerText: '#f00'
          },
          overlayOpacity: 0.5, // 0.5 as default
          dismissible: true // as true as default
        },
      }
    },
    watch: {
      keyword () {
        this.getTableData()
      }
    },
    methods: {
      onParamChange(data) {

        this.productTye = data.value
        this.getTableData()
      },
      getTableData() {
        let reqParam = {
          startDate: this.startDate.time,
          endDate: this.endDate.time,
          keyword: this.keyword,
          productTye: this.productTye
        }
        this.$http.post('/api/getOrderList', reqParam)
          .then((res) => {
          this.tableData = res.data.data.list;
          })
      }
    },
    mounted() {
      this.getTableData()
    }
  }
</script>

<style scoped>
  .order-wrap {
    width: 1200px;
    min-height: 750px;
    margin: 20px auto;
  }

  .search-wrap {
    font-size: 0;
    letter-spacing: -3px;
    margin-bottom: 20px;
  }

  .selection {
    width: 25%;
    display: inline-block;
    vertical-align: middle;
    height: 40px;
    line-height: 40px;
    font-size: 14px;
    letter-spacing: 1px;
  }

  .keyword {
    border: 1px solid #e3e3e3;
    height: 25px;
    line-height: 25px;
    padding-left: 5px;
    width: calc(100% - 100px);
    min-width: 100px;
  }

  .order-list {
    width: 100%;
    margin: 0 auto;
    border-radius: 3px;
  }

  .order-list th{
    height: 35px;
    line-height: 35px;
    text-align: center;
    color: #fff;
    background-color: #31c1a6;
    border-right: 1px solid #fff;
  }

  .order-list th:last-child {
    border-right: none;
  }

  .order-list td{
    height: 35px;
    line-height: 35px;
    text-align: center;
    color: #666666;
    background-color: #fff;
    border-right: 1px dotted #e3e3e3;
    border-bottom: 1px dotted #e3e3e3;
  }

  .order-list tr:hover {
    background-color: beige;
  }


</style>
