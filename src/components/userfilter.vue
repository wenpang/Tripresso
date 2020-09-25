<template>
  <!-- 篩選菜單 -->
  <div class="col-md-3 col-12">
    <div class="card">
      <div class="card-header">
        <strong>篩選項目</strong>
      </div>
      <div class="card-body">
        <p class="card-text">
          <i class="far fa-calendar-alt"></i>
          <b>出發日期</b>
        </p>
        <div class="block">
          <el-date-picker
            style="width: 250px"
            size="small"
            v-model="value1"
            type="daterange"
            range-separator=" - "
            start-placeholder="开始日期"
            end-placeholder="结束日期">
          </el-date-picker>
        </div>
        <hr/>
        <p class="card-text">
          <i class="far fa-compass"></i>
          <b>目地的</b>
        </p>
        <el-checkbox-group v-model="location">
          <el-checkbox>{{city}}</el-checkbox>
        </el-checkbox-group>
        <hr/>
        <p class="card-text">
          <i class="fas fa-dollar-sign"></i>
          <b>價格</b>
        </p>
        <div class="block">
          <el-slider
            v-model="money"
            range
            show-stops
            input-size="small"
            :max="5000">
          </el-slider>
        </div>
        <hr/>
        <p class="card-text">
          <i class="far fa-clock"></i>
          <b>天數</b>
        </p>
        <el-checkbox-group v-model="date" v-for="item of dateList" :key="item">
          <el-checkbox :value="item">{{ item }}</el-checkbox>
        </el-checkbox-group>
      </div>
    </div>
  </div>
</template>

<script>
    export default {
        name: "userfilter",
        data(){
          return{
            value1: '',
            city: '港澳中國',
            location: '',
            money: [0, 500],
            date: '',
            dateList: ['5天以下','6-8天']
          }
        }
    }
</script>

<style scoped>

</style>
