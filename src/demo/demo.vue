<template>
  <div class="content">
    <!-- agoDayHide='1517483961' -->
    <!-- futureDayHide="1526054400" -->
    <Calendar
      ref="Calendar"
      :markDateMore="arr"
      :markDate="arr2"
      v-on:isToday="clickToday"
      agoDayHide="1530115221"
      v-on:choseDay="clickDay"
      v-on:changeMonth="changeDate"
    ></Calendar>
    <br>
    <h3 @click="demo">markDateMore 标记不同风格</h3>
    <br>
    <h3>markDate 标记单一风格</h3>
    <div style="margin:20px auto;text-align:center;">
      <input type="text" v-model="input" style="height:30px;padding:0 10px;">
      <h3 style="margin-top:20px;">格式为：yyyy-MM-dd</h3>
    </div>
    <div class="div" @click="demo">点击跳到指定日期</div>
  </div>
</template>

<script>
import Calendar from '../vue-calendar-component/index';
// import Calendar from "vue-calendar-component";
export default {
  data() {
    return {
      // arr2: ['2018/6/23'],
      arr2: [],
      arr: [
        {
          date: "2018/8/1",
          className: "calendar-mark-notstarted"
        },
        {
          date: "2018/8/13",
          className: "calendar-mark-end"
        }
      ],
      input: ''
    }
  },
  components: {
    Calendar
  },
  methods: {
    clickDay(data) {
      console.log("选中了", data); //选中某天
      this.$toast("选中了" + data);
    },
    clickToday(data) {
      console.log("跳到了本月今天", data); //跳到了本月
    },
    changeDate(data) {
      this.$toast("切换到的月份为" + data);
      console.log("左右点击切换月份", data); //左右点击切换月份
    },
    demo() {
      this.$refs.Calendar.ChoseMonth(this.input); //跳到12月12日选中12月12日
    }
  },
  created() {
    function format(date, index) {
      date = new Date(date);
      return `${date.getFullYear()}-${date.getMonth() + 1}-${index}`;
    }
    setTimeout(() => {
      this.arr = [
        {
          date: format(new Date(), 3),
          className: "calendar-mark-notstarted"
        },
        {
          date: format(new Date(), 12),
          className: "calendar-mark-end"
        }
      ];
      this.arr.push({
        date: format(new Date(), 15),
        className: "calendar-mark-notstarted"
      });
    }, 300);
  }
};
</script>

<!-- Add "scoped " attribute to limit CSS to this component only -->
<style scoped>
.content {
  margin-top: 50px;
}
h3 {
  text-align: center;
  width: 90%;
  margin: auto;
}

.div {
  margin: auto;
  width: 220px;
  height: 44px;
  line-height: 44px;
  background: #00c3d0;
  color: #fff;
  font-size: 17px;
  text-align: center;
  margin-top: 20px;
}
</style>