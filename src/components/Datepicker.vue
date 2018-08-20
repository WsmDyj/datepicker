<template>
<div id="calendar">
    <div class="month">
        <ul>
            <li class="arrow" @click="pickPre(currentYear,currentMonth)">❮</li>
            <li class="year-month">
                <span class="choose-year">{{ currentYear }}</span>
                <span class="choose-month">{{ currentMonth }}月</span>
            </li>
            <li class="arrow" @click="pickNext(currentYear,currentMonth)">❯</li>
        </ul>
    </div>
    <!-- 星期 -->
    <ul class="weekdays">
        <li>一</li>
        <li>二</li>
        <li>三</li>
        <li>四</li>
        <li>五</li>
        <li style="color:red">六</li>
        <li style="color:red">日</li>
    </ul>
    <!-- 日期 -->
    <ul class="days">
        <!-- v-for循环 每一次循环用<li>标签创建一天 -->
        <li  v-for="(dayobject,index) in days" :key="index" style="height: 50px;"  @click="pickDay(dayobject)">
            <!--本月-->
            <!--如果不是本月  改变类名加灰色-->
            <span v-if="dayobject.day.getMonth()+1 != currentMonth" class="other-month">{{ dayobject.day.getDate() }}</span>
            <!--如果是本月  还需要判断是不是这一天-->
            <span v-else>
          <!--今天  同年同月同日-->
              <span v-if="dayobject.day.getFullYear() == new Date().getFullYear() &&  
              dayobject.day.getMonth() == new Date().getMonth() && 
              dayobject.day.getDate() == new Date().getDate()" class="active">{{ dayobject.day.getDate() }}</span>
              <span v-else>{{ dayobject.day.getDate() }}</span>
            </span>
        </li>
    </ul>
    <div class="select">
    <span>选择的日期为：</span>
    <input type="text" :value="select">
  </div>
</div>
</template>
<script>
import { mixinDate } from '../mixins/index'
import BScroll from 'better-scroll';
export default {
  mixins: [mixinDate],
  data () {
    return {
      currentWeek: 1,
      currentDay: 1,
      currentMonth: 1,
      currentYear: 1970,
      select: ''
    }
  },
  methods: {
    pickDay (dayobject) {
       this.select =this.currentYear + "-" + (dayobject.day.getMonth()+1) + "-" + dayobject.day.getDate()
    },
  }
};
</script>
<style>
* {
  box-sizing: border-box;
}
ul {
  list-style-type: none;
}
body {
  font-family: Verdana, sans-serif;
  background: #e8f0f3;
}

#calendar {
  display:inline-block;
  margin-left: 20px;
  width: 40%;
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.14), 0 3px 1px -2px rgba(0, 0, 0, 0.1),
    0 1px 5px 0 rgba(0, 0, 0, 0.12);
}
.select {
  text-align: center;
}
.selected {
  padding: 6px 10px;
  border-radius: 50%;
  background: red;
  color: #fff;
}
input {
    width:20%;
    padding-left: 5px;
    line-height: 24px;
    border: 1px solid #BFCBD7;
    border-radius: 3px;
    font-size: 14px;
    outline: none;
    cursor: pointer;
}
input:focus {
    border: 1px solid #20a0ff;
}
.month {
  width: 100%;
  background: #00b8ec;
}
.month ul {
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: space-between;
}
.year-month {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}
.year-month:hover {
  background: rgba(150, 2, 12, 0.1);
}
.choose-year {
  padding-left: 20px;
  padding-right: 20px;
}
.choose-month {
  text-align: center;
  font-size: 1.5rem;
}
.arrow {
  padding: 30px;
}
.arrow:hover {
  background: rgba(100, 2, 12, 0.1);
}
.month ul li {
  color: white;
  font-size: 20px;
  text-transform: uppercase;
  letter-spacing: 3px;
}
.weekdays {
  margin: 0;
  padding: 10px 0;
  background-color: #00b8ec;
  display: flex;
  flex-wrap: wrap;
  color: #ffffff;
  justify-content: space-around;
}
.weekdays li {
  display: inline-block;
  width: 13.6%;
  text-align: center;
}
.days {
  padding: 0;
  background: #ffffff;
  margin: 0;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}
.days li {
  list-style-type: none;
  display: inline-block;
  width: 14.2%;
  text-align: center;
  padding-top: 15px;
  color: #000;
}
.days li .active {
  padding: 6px 10px;
  border-radius: 50%;
  background: #00b8ec;
  color: #fff;
}
.active {
  background: #00b8ec;
  width: 100%;
  color: #fff;
  
}
.days li .other-month {
  padding: 5px;
  color: gainsboro;
}
.days li:hover {
  background: #e1e1e1;
}
.year-panel {
  width: 50%;
  height: 300px;
  overflow: hidden;
  border-right: 1px solid #00b8ec;
  float: left;
  background: #fff;
}
.item:hover {
  background: rgba(150, 2, 12, 0.1);
}
.item {
  padding: 9px;
  font-size: 16px;
  width: 100%;
  line-height: 20px;
}
.month-panel {
  width: 50%;
  height: 300px;
  overflow: hidden;
  float: right;
  background: #fff;
}

</style>

