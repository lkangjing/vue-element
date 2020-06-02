<template>
  <div class="calendar-header">

    <div class="toggle-month">
      <i class="prev" @click="handlerPrevMonth">&lt;</i>
      <span class="center">{{ currentDate.year }} / {{ currentDate.month + 1 }}</span>
      <i class="next" @click="handlerNextMonth">&gt;</i>
    </div>
    <div class="conut">
      <i class="event-dot" />任务数：<span class="num">2</span>
    </div>
    <router-link to="/example/map" class="add">+</router-link>
  </div>
</template>

<script>
export default {
  props: {
    // eslint-disable-next-line vue/require-default-prop
    currentDate: Object
  },
  methods: {
    handlerPrevMonth() {
      this.$emit('handlerPrevMonth')
    },
    handlerNextMonth() {
      console.log(this.currentDate)

      this.$emit('handlerNextMonth')
      console.log(this.currentDate)
    }
  }

}
</script>

<style scoped>
.calendar-header {
    position: relative;
    border: 1px solid #E4E7EA;
    height: 47px;
    background-color: #8696b1;
    text-align: center;
    line-height: 45px;
}
.prev {
    cursor: pointer;
    font-size: 20px;
    font-weight: 700;
}
.next {
    cursor: pointer;
    font-size: 20px;
    font-weight: 700;

}
.center {
    color: #fff;
    margin: 0 10px;
    font-size: 18px;
}
.conut {
    position: absolute;
    width: 100px;
    height: 45px;
    line-height: 45px;
    right: 15%;
    top: 0px;
    font-size: 14px;
    color: #fff;
}
.num {
    color: #333;
    font-size: 20px;
    font-weight: 700;
    vertical-align: middle;
}
.add {
    position: absolute;
    top: 0;
    right: 5%;
    width: 20px;
    height: 45px;
    font-size: 30px;
    color: #fff;
    text-decoration: none;
}
.event-dot {
    display: inline-block;
    width: 10px;
    height: 10px;
    border-radius: 50%;
    border: 1px solid rgba(255,255,255,.5);
    background: #009ad8;
    box-shadow: 0 0 5px 0px #009ad8;
    margin-right: 10px;
}
</style>
