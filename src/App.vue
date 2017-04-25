<template>
  <div id="app">
    <div class="title">三级地址联动：</div>
    <address-select
      :province="form.province"
      :city="form.city"
      :area="form.area"
      v-on:updateprovice="listenProvice"
      v-on:updatecity="listenCity"
      v-on:updatearea="listenArea"></address-select>
    <el-button type="primary" @click="confirm" class="comfirmbtn">确认</el-button>
  </div>
</template>

<script>
import Address from '@/components/address.vue';

export default {
  data() {
    return {
      form : {
        province: '广东省',
        city: '广州市',
        area: '荔湾区'
      }
    };
  },
  components: {
    'address-select': Address
  },
  methods: {
    listenProvice(val) {
      this.form.province = val;
    },
    listenCity(val) {
      this.form.city = val;
    },
    listenArea(val) {
      this.form.area =val;
    },
    confirm() {
      this.$alert(`你选择了${this.form.province} ${this.form.city} ${this.form.area}`,'提示', {
        confirmButtonText: '确定'
      });
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
.title{
  line-height: 50px;
  text-align: left;
  font-weight: bold;
  font-size: 18px;
  text-indent: 5px;

}
.el-button.comfirmbtn{
  margin-top: 20px;
}
</style>
