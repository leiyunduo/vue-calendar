<style scoped>
@media screen and (min-width: 460px) {
  .wh_item_date:hover {
    background: #71c7a5;
    cursor: pointer;
  }
}
* {
  margin: 0;
  padding: 0;
}

li {
  list-style-type: none;
}
.wh_top_changge .wh_content_li {
  cursor: auto;
  flex: 2.5;
}
.wh_content {
  display: flex;
  flex-wrap: wrap;
  padding: 0 3% 0 3%;
  width: 100%;
}
/* 左右箭头 */
.wh_jiantou1 {
  width: 10px;
  height: 10px;
  border-top: 2px solid #000;
  border-left: 2px solid #000;
  transform: rotate(-45deg);
}

.wh_jiantou2 {
  width: 10px;
  height: 10px;
  border-top: 2px solid #000;
  border-right: 2px solid #000;
  transform: rotate(45deg);
}

/* 上个月末尾-下个月月初 */
.wh_content_item .wh_other_dayhide {
  color: #bfbfbf;
}
/* 无法选中 */
.wh_content_item .wh_want_dayhide {
  color: #bfbfbf;
}
.wh_container {
  max-width: 410px;
  margin: auto;
  height: 333px;
  border-bottom: 1px solid #e9e9e9 !important;
}
.wh_container .wh_content_all {
  background-color: #fff;
  width: 100%;
  overflow: hidden;
  padding-bottom: 8px;
  font-family: -apple-system, BlinkMacSystemFont, "PingFang SC",
    "Helvetica Neue", STHeiti, "Microsoft Yahei", Tahoma, Simsun, sans-serif;
}
.wh_content .wh_content_item .wh_top_tag {
  width: 40px;
  height: 40px;
  line-height: 40px;
  margin: auto;
  display: flex;
  justify-content: center;
  align-items: center;
}
.wh_content_item {
  height: 40px;
}
.wh_content_item, .wh_content_item_tag {
  width: 13.4%;
  text-align: center;
  position: relative;
  font-size: 13px;
  color: #000000;
  font-family: "Sim Hei";
}
.wh_container .wh_content_all .wh_top_changge {
  height: 30px;
  border-bottom: 1px solid #c6c9cb;
  background: #edf3f7;
  line-height: 30px;
  display: flex;
}
.wh_container .wh_content_all .wh_top_changge li {
  height: 30px;
  line-height: 30px;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  flex: 1;
}
.wh_container .wh_content_all .wh_top_changge .wh_content_li {
  color: #333;
  font-size: 16px;
  cursor: auto;
  flex: 2.5;
}
.wh_container .wh_content_all .wh_content:nth-of-type(2) {
  height: 44px;
  border-bottom: 1px solid #e9e9e9;
}
.wh_container .wh_content_all .wh_content:nth-of-type(3) .wh_content_item {
  font-size: 12px;
  color: #404040;
  font-family: "Sim Hei";
}
/* 今天 */
.wh_container .wh_content_all .wh_content_item .wh_isToday {
  background: #fff;
}
.wh_container .wh_content_all .wh_content_item .wh_item_date {
  width: 20px;
  height: 20px;
  text-align: center;
  margin: 14px 0 7px 18px;
  display: flex;
  justify-content: center;
  align-items: center;
}
/* 默认选中的 */
.wh_container .wh_content_all .wh_content_item .wh_item_date:hover {
  background: #00c3d0;
  cursor: pointer;
  color: #fff;
  border-radius: 100px;
  border: 1px solid #00c3d0;
  box-sizing: border-box;
}
.wh_container .wh_content_all .wh_content_item>.calendar-mark-end {
  border-radius: 100px;
  background: none;
  border: 1px solid #999999;
  box-sizing: border-box;
  text-align: center;
  color: #999999;
}
.wh_container .wh_content_all .wh_content_item>.calendar-mark-notstarted {
  border-radius: 100px;
  background: #fff;
  border: 1px solid #00c3d0;
  box-sizing: border-box;
  text-align: center;
  color: #333;
}
/* 选中时的颜色 */
.wh_container .wh_content_all .wh_content_item .wh_chose_day {
  border-radius: 100px;
  background: #00c3d0;
  border: none;
  box-sizing: border-box;
  text-align: center;
  color: #fff;
}
/* 不属于本月的日期显示样式 */
.wh_container .wh_content_all .wh_content_item .wh_other_dayhide {
  background: none;
  border: none;
  box-sizing: border-box;
  text-align: center;
  color: #bfbfbf;
  pointer-events: none;
  cursor: not-allowed;
}
</style>
<template>
  <section class="wh_container">
    <div class="wh_content_all">
      <div class="wh_top_changge">
        <li @click="PreMonth(myDate,false)" v-if="leftRightHide">
          <div class="wh_jiantou1"></div>
        </li>
        <li class="wh_content_li">{{dateTop}}</li>
        <li @click="NextMonth(myDate,false)" v-if="leftRightHide">
          <div class="wh_jiantou2"></div>
        </li>
      </div>
      <div class="wh_content">
        <div class="wh_content_item" v-for="tag in textTop">
          <div class="wh_top_tag">{{tag}}</div>
        </div>
      </div>
      <div class="wh_content">
        <div class="wh_content_item" v-for="(item,index) in list" @click="clickDay(item,index)">
          <div
            class="wh_item_date"
            v-bind:class="[{ wh_isMark: item.isMark},{wh_other_dayhide:item.otherMonth!=='nowMonth'},{wh_want_dayhide:item.dayHide},{wh_isToday:item.isToday},{wh_chose_day:item.chooseDay},setClass(item)]"
          >{{item.id}}</div>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
import timeUtil from "./calendar";
export default {
  data() {
    return {
      myDate: [],
      list: [],
      historyChose: [],
      dateTop: ""
    };
  },
  props: {
    markDate: {
      type: Array,
      default: () => []
    },
    markDateMore: {
      type: Array,
      default: () => []
    },
    textTop: {
      type: Array,
      default: () => ["一", "二", "三", "四", "五", "六", "日"]
    },
    sundayStart: {
      type: Boolean,
      default: () => false
    },
    agoDayHide: {
      type: String,
      default: `0`
    },
    futureDayHide: {
      type: String,
      default: `2554387200`
    },
    // 切换左右按钮是否显示
    leftRightHide: {
      type: Boolean,
      default: () => true
    }
  },
  created() {
    this.intStart();
    this.myDate = new Date();
  },
  methods: {
    intStart() {
      timeUtil.sundayStart = this.sundayStart;
    },
    setClass(data) {
      let obj = {};
      obj[data.markClassName] = data.markClassName;
      return obj;
    },
    clickDay: function(item, index) {
      if (item.otherMonth === "nowMonth" && !item.dayHide) {
        this.getList(this.myDate, item.date);
      }
      // 上个月末尾的日期与下个月末尾的日期是否可以切换
      // if (item.otherMonth !== "nowMonth") {
      //   item.otherMonth === "preMonth"
      //     ? this.PreMonth(item.date)
      //     : this.NextMonth(item.date);
      // }
    },
    ChoseMonth: function(date, isChosedDay = true) {
      date = timeUtil.dateFormat(date);
      this.myDate = new Date(date);
      this.$emit("changeMonth", timeUtil.dateFormat(this.myDate));
      if (isChosedDay) {
        this.getList(this.myDate, date, isChosedDay);
      } else {
        this.getList(this.myDate);
      }
    },
    PreMonth: function(date, isChosedDay = true) {
      date = timeUtil.dateFormat(date);
      this.myDate = timeUtil.getOtherMonth(this.myDate, "preMonth");
      this.$emit("changeMonth", timeUtil.dateFormat(this.myDate));
      if (isChosedDay) {
        this.getList(this.myDate, date, isChosedDay);
      } else {
        this.getList(this.myDate);
      }
    },
    NextMonth: function(date, isChosedDay = true) {
      date = timeUtil.dateFormat(date);
      this.myDate = timeUtil.getOtherMonth(this.myDate, "nextMonth");
      this.$emit("changeMonth", timeUtil.dateFormat(this.myDate));
      if (isChosedDay) {
        this.getList(this.myDate, date, isChosedDay);
      } else {
        this.getList(this.myDate);
      }
    },
    forMatArgs: function() {
      let markDate = this.markDate;
      let markDateMore = this.markDateMore;
      markDate = markDate.map(k => {
        return timeUtil.dateFormat(k);
      });
      markDateMore = markDateMore.map(k => {
        k.date = timeUtil.dateFormat(k.date);
        return k;
      });
      return [markDate, markDateMore];
    },
    getList: function(date, chooseDay, isChosedDay = true) {
      const [markDate, markDateMore] = this.forMatArgs();
      this.dateTop = `${date.getFullYear()}年${date.getMonth() + 1}月`;
      let arr = timeUtil.getMonthList(this.myDate);
      for (let i = 0; i < arr.length; i++) {
        let markClassName = "";
        let k = arr[i];
        k.chooseDay = false;
        const nowTime = k.date;
        const t = new Date(nowTime).getTime() / 1000;
        //看每一天的class
        for (const c of markDateMore) {
          if (c.date === nowTime) {
            markClassName = c.className || "";
          }
        }
        //标记选中某些天 设置class
        k.markClassName = markClassName;
        k.isMark = markDate.indexOf(nowTime) > -1;
        //无法选中某天
        k.dayHide = t < this.agoDayHide || t > this.futureDayHide;
        if (k.isToday) {
          this.$emit("isToday", nowTime);
        }
        let flag = !k.dayHide && k.otherMonth === "nowMonth";
        if (chooseDay && chooseDay === nowTime && flag) {
          this.$emit("choseDay", nowTime);
          this.historyChose.push(nowTime);
          k.chooseDay = true;
        } else if (
          this.historyChose[this.historyChose.length - 1] === nowTime &&
          !chooseDay &&
          flag
        ) {
          k.chooseDay = true;
        }
      }
      this.list = arr;
    }
  },
  mounted() {
    this.getList(this.myDate);
  },
  watch: {
    markDate: {
      handler(val, oldVal) {
        this.getList(this.myDate);
      },
      deep: true
    },
    markDateMore: {
      handler(val, oldVal) {
        this.getList(this.myDate);
      },
      deep: true
    },
    agoDayHide: {
      handler(val, oldVal) {
        this.getList(this.myDate);
      },
      deep: true
    },
    futureDayHide: {
      handler(val, oldVal) {
        this.getList(this.myDate);
      },
      deep: true
    },
    sundayStart: {
      handler(val, oldVal) {
        this.intStart();
        this.getList(this.myDate);
      },
      deep: true
    }
  }
};
</script>