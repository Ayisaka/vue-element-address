<!-- 地址选择组件 -->
<template>
  <el-form :model="form" class="demo-ruleForm" ref="form" label-position="top">
  <el-row :gutter="10" class="address">
      <el-col :span="3">
        <el-form-item  prop="province">
        <el-select v-model="form.province" name="province" placeholder="请选择省" @change="proChange" >
          <el-option
            v-for="item in provinces"
            :key="item.value"
            :value="item.value">
          </el-option>
        </el-select>
        </el-form-item>
      </el-col>
    <el-col :span="3">
      <el-form-item   prop="city">

      <el-select v-model="form.city" name="city" placeholder="请选择市" @change="cityChange" >
        <el-option
          v-for="item in citys"
          :key="item.value"
          :value="item.value">
        </el-option>
      </el-select>
      </el-form-item>
    </el-col>
    <el-col :span="3">
      <el-form-item prop="area">
      <el-select v-model="form.area" name="area" placeholder="请选择区" @change="areaChange">
        <el-option
          v-for="item in areas"
          :key="item.value"
          :value="item.value">
        </el-option>
      </el-select>
      </el-form-item>
    </el-col>
  </el-row>
</el-form>
</template>
<script>
  import addressData from '@/components/addressData.js'

  function formatData(data){
    var result = [];
    for(var key in data){
      result.push({
        value: key
      })
    }
    return result
  }

  export default {
    name:'address',
    props:['province','city','area'],
    data: function () {
      return {
        form:{
          province: this.province,
          city: this.city,
          area: this.area,
        },
        provinces: formatData(addressData)
      };
    },
    computed: {
      provinces: function () {
        formatData(addressData);
      },
      citys: function (){
        if(this.form.province) {
          return formatData(addressData[this.form.province]);
        }
      },
      areas: function() {
        if(this.form.province && this.form.city) {
          var areaslit = [];
          var areadata = addressData[this.form.province][this.form.city];
          for(var key in areadata) {
            areaslit.push({
              value: areadata[key]
            })
          }
          return areaslit;
        }
      }
    },
    methods: {
      proChange: function (val,oldVal) {
        if(val !== this.province){
          this.form.city='';
          this.form.area='';
        }
        this.$emit('updateprovice', this.form.province);
        var data = formatData(addressData[this.form.province]);
        for(var i =0; i<data.length; i++){
          this.$set(this.citys,i,data[i]);
        }
      },
      cityChange: function (val, oldVal) {
        if (val !== this.city) {
          this.form.area='';
        }
        this.$emit('updatecity', this.form.city);
      },
      areaChange: function () {
        this.$emit('updatearea', this.form.area);
      }
    },
    watch: {
      province: function (val,  oldVal) {
        this.form.province = val;
      },
      city: function (val,  oldVal) {
        this.form.city = val;
      },
      area: function (val,  oldVal) {
        this.form.area = val;
      },

    }
  }
</script>
<style>
  .address{}
  .address .el-form-item{margin-bottom: 0!important;margin-right: 0!important;}
</style>
