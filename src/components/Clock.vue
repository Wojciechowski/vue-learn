<template>
  <h1>Clock</h1>
  <div class="clock">
    <p>
      Current Date & Time: {{ dateTime }}<br>
      Secounds: {{ counter }}
    </p>
    <div class="pannikin">
<!--      <div v-for="n in 6" :key="n">-->
      <div v-for="n in 6" :key="n" :style="{ transform: 'rotate('+ (30 * n) +'deg)'}">
        <span>{{ n }}</span>
        <span>{{ n + 6 }}</span>
      </div>
    </div>
    <div class="hour-hand hands-clock" :style="{ transform: 'rotate('+ hourDeg +'deg)'}"></div>
    <div class="minutes-hand hands-clock" :style="{ transform: 'rotate('+ minuteDeg +'deg)'}"></div>
    <div class="seconds-hand hands-clock" :style="{ transform: 'rotate('+ secondsDeg +'deg)'}"></div>
  </div>
</template>

<script>
export default {
  name: "Clock",
  data() {
    return {
      counter: 0,
      hourDeg: 0,
      minuteDeg: 0,
      secondsDeg: 0,
      dateTime: ''
    }
  },
  methods: {
    callFunction: function () {
      var currentDate = new Date();
      alert(currentDate);
      var currentDateWithFormat = new Date().toJSON().slice(0, 10).replace(/-/g, '/');
      console.log('DATE', currentDateWithFormat);
    },
  },
  mounted() {
    this.callFunction(),
        setInterval(() => {
          const current = new Date();
          const date = current.getFullYear() + '-' + (current.getMonth() + 1) + '-' + current.getDate();
          // const unit = 6;
          const hour = current.getHours();
          const hour12 = hour / 2;
          this.hourDeg = 6 * hour12;
          const minutes = current.getMinutes();
          this.minuteDeg = 6 * minutes;
          const seconds = current.getSeconds();
          this.secondsDeg = 6 * seconds;
          const time = hour + ":" + minutes + ":" + seconds;
          this.dateTime = date + ' ' + time;
          this.counter = seconds;
        }, 500)
  }
}
</script>

<style scoped lang="scss">
$clock-size: 250px;
.clock {
  position: relative;
  background-color: #f7ebaa;
  border: 1px solid #becbd0;
  box-shadow: 1px 1px 0 8px rgba(0, 0, 0, 0.5);
  margin: 0 auto;

  &,
  .hands-clock {
    border-radius: 50%;
    height: $clock-size;
    width: $clock-size;
  }

  .hands-clock {
    position: absolute;
    left: 0;
    top: 0;

    &:before,
    &:after {
      content: '';
      position: absolute;
      box-shadow: 0 0 5px rgb(0 0 0 / 50%);
      left: 50%;

    }

    &:after {
      content: '';
      border-radius: 50%;

    }
  }

  .pannikin {
    &,
    & > div{
      position: absolute;
      height: 100%;
      width: 30px;
      top: 0;
      left: 50%;
      margin-left: -15px;

      span {
        position: absolute;
        background-color: white;
        border-radius: 50%;
        width: 30px;
        height: 30px;
        left: 0;
        line-height: 30px;
        font-weight: bold;
        text-align: center;

        & + span {
          bottom: 0;
        }
      }
    }
  }

  p {
    margin-top: 150px;
    text-align: center;
  }

  .seconds-hand {
    z-index: 3;

    &:before {
      background-color: red;
      width: 3px;
      height: 68%;
      top: -8px;
      margin-left: -1.5px;
    }

    &:after {
      background-color: black;
      border: 4px solid red;
      height: 1px;
      width: 1px;
      top: 50%;
      margin-left: -2.8px;
      margin-top: -2.8px;
    }
  }

  .minutes-hand {
    z-index: 2;

    &:before {
      background-color: black;
      width: 5px;
      height: 65%;
      top: 5px;
      margin-left: -2.5px;
    }

    &:after {
      background-color: black;
      border-radius: 50%;
      height: 18px;
      width: 18px;
      top: 50%;
      margin-left: -9px;
      margin-top: -9px;
    }
  }

  .hour-hand {
    z-index: 1;

    &:before {
      background-color: black;
      width: 8px;
      height: 52%;
      top: 24px;
      margin-left: -4px;
    }

  }
}
</style>
