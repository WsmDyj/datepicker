<template>
<div id="calendar">
   <!-- 年份 月份 -->
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
  <div class="date-wrapper">
    <!-- 滚动年 -->
    <div  class="year-panel" ref="wrapper">
      <ul>
          <li class="item" v-for="(y,index) of years" :key="index"
          @click.stop="pickYear(y)" :class="{'active': y == currentYear}">{{y}}</li>
      </ul>
    </div>
    <!-- 滚动月 -->
    <div  class="month-panel" ref="month">
      <ul>
          <li class="item" v-for="(m,$index) of months" :key="$index"
            @click.stop="pickMonth($index + 1)" :class="{'active': m == currentMonth}" >{{m}}月</li>
      </ul>
    </div>
    <!-- 滚动日 -->
    <!-- <div class="day-panel" ref="day">
      <ul>
        <li class="item" v-for="(d,index) in days" :key="index" :class="{'active': d.day.getDate() == new Date().getDate()}"
            @click.stop="pickDay(d)">{{ d.day.getDate() }}</li>
      </ul>
    </div> -->
  </div>
  <div class="select">
    <span>选择的日期为：</span>
    <input type="text" :value="current">
  </div>
</div>
</template>
<script>
import { mixinDate } from "../mixins/index";
import BScroll from "better-scroll";
export default {
  mixins: [mixinDate],
  data() {
    return {
      years: [],
      months: []
    };
  },
  created() {
    for (let i = 2015; i <= 2100; i++) {
      this.years.push(i);
    }
    for (let j = 1; j <= 12; j++) {
      this.months.push(j);
    }
  },
  methods: {
    // 选取年
    pickYear(y) {
      this.currentYear = y;
      this.current = this.currentYear+ "-" + this.currentMonth;
    },
    // 选取月
    pickMonth(m) {
      this.currentMonth = m;
      this.current = this.currentYear + "-" + this.currentMonth;
    },
    pickDay(d) {
      this.currentDay = d.day.getDate();
      this.current = this.currentYear + "-" + this.currentMonth + "-" + d.day.getDate();
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.scroll = new BScroll(this.$refs.wrapper);
      this.scroll = new BScroll(this.$refs.month);
      this.scroll = new BScroll(this.$refs.day);
    });
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
  display: inline-block;
  width: 40%;
  margin-left: 20px;
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.14), 0 3px 1px -2px rgba(0, 0, 0, 0.1),
    0 1px 5px 0 rgba(0, 0, 0, 0.12);
}
.select {
  text-align: center;
}
input {
  width: 30%;
  padding-left: 5px;
  border: 1px solid #bfcbd7;
  border-radius: 3px;
  font-size: 14px;
  outline: none;
  cursor: pointer;
  margin: 6px 0;
}
input:focus {
  border: 1px solid #20a0ff;
}


</style>
