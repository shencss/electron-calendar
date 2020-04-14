<template>
  <div class="calendar">
    <div class="title"> Calendar For 47 <span>❤</span></div>
    <div class="content">
      <div class="date">
        <div class="day">
          <div class="book">
            <div class="header">
              <div class="left-line"></div>
              <div class="month-num">{{month}}</div>
              <div class="right-line"></div>
            </div>
            <div class="day-num">{{day}}</div>
          </div>
        </div>
      </div>
      <div class="time">
        <div class="hour">{{hour}}</div>
        <span>:</span>
        <div class="minute">{{minute}}</div>
        <span>:</span>
        <div class="second">{{second}}</div>
      </div>
      <div class="weather">
        <div>天气：{{weather.type}}</div>
        <div>温度：{{weather.low.slice(2)}}~{{weather.high.slice(2)}}</div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    name: 'landing-page',
    data () {
      return {
        month: '',
        day: '',
        hour: '',
        minute: '',
        second: '',
        period: '',
        weather: null
      }
    },
    methods: {
      refreshDate () {
        const monthMap = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'June', 'July', 'Aug', 'Sept', 'Oct', 'Nov', 'Dec']
        const now = new Date()
        this.month = monthMap[now.getMonth()]
        this.day = now.getDate()
        const hour = now.getHours()
        const minute = now.getMinutes()
        const second = now.getSeconds()
        this.hour = hour < 10 ? '0' + hour : hour
        this.minute = minute < 10 ? '0' + minute : minute
        this.second = second < 10 ? '0' + second : second
        setTimeout(() => {
          this.refreshDate()
        }, 1000)
      },
      judgePeriod (day) {
        if (day >= (this.period + 2) && day <= (this.period - 2)) {
          // todo：大姨妈提示
        }
      },
      judgeOvertime (hour, minute, second) {
        if (hour === 18 && minute === 30 && second === 0) {
          // todo：下班提示
        } else if (hour === 19 && minute === 0 && second === 0) {
          // todo：吃饭提示
        } else if (hour === 21 && minute === 0 && second === 0) {
          // todo：加班安慰
        } else if (hour === 23 && minute === 0 && second === 0) {
          // todo：超级辛苦
        }
      },
      judgeBirthday (month, day) {
        if (month === 8 && day === 4) {
          // todo：生日快乐
        }
      },
      greeting (hour, minute, second) {
        // todo：早晚午安
      },
      ticket (date, hour, minute, second) {
        // todo：车票提示
      },
      anniversary (year, month, day) {
        // todo：纪念日
      },
      weather (tomorrow) {
        // todo：带伞提示
      }
    },
    created () {
      this.period = +localStorage.getItem('period') || 22
      this.refreshDate()
      axios.get('http://wthrcdn.etouch.cn/weather_mini?citykey=101280101').then(res => {
        this.weather = res.data.data.forecast[0]
      })
    }
  }
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  body { font-family: 'Source Sans Pro', sans-serif; }
  .calendar {
    position: relative;
    box-shadow: 0 0 10px rgba(0, 0, 0, .5);
    height: 100%;
    width:100%;
    border-radius: 8px;
    overflow: hidden;
  }
  .title {
    text-align: center;
    color: royalblue;
    height: 25px;
    line-height: 25px;
    background:#fff;
    font-weight: bold;
  }
  .title span {
    display: inline-block;
    -webkit-app-region: no-drag;
    cursor: pointer;
    transition: all linear .1s;
    user-select: none;
  }
  .title  span:hover {
    transform: scale(1.5);
  }
  .date {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 5px;
  }
  .day {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    background-color: rgb(116, 173, 202);
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .book {
    width: 65px;
    height: 65px;
    border-radius: 5px;
    background-color: #fff;
  }
  .book .header {
    position: relative;
    height: 20px;
    width: 100%;
    border-radius: 5px 5px 0 0;
    background-color: rgb(193, 89, 89);
  }
  .book .header .left-line {
    position: absolute;
    top: -8px;
    left: 8px;
    width: 6px;
    height: 16px;
    border-radius: 3px;
    background-color:rgb(224, 222, 207);
  }
  .book .header .right-line{
    position: absolute;
    top: -8px;
    right: 8px;
    width: 6px;
    height: 16px;
    border-radius: 3px;
    background-color:rgb(224, 222, 207);
  }
  .book .month-num {
    text-align: center;
    color: #fff;
    font-size: 14px;
    font-weight: bold;
  }
  .book .day-num {
    line-height: 45px;
    height: 45px;
    text-align: center;
    font-size: 30px;
    font-weight: bold;
    color: rgb(77, 92, 115);
  }
  .time {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 8px;
    font-size: 28px;
    color: #fff;
    font-weight: bold;
  }
  .weather {
    position: absolute;
    top: 70px;
    font-size: 12px;
    color: #fff;
    font-weight: bold;
  }
</style>
