<template>
  <ul class="calendar-week">
    <li class="week-item" v-for="(week, index) in weekData" :key="index">{{week}}</li>
  </ul>
</template>

<script>
export default {
  data () {
    return {
      weekData: ['周日', '周一', '周二', '周三', '周四', '周五', '周六']
    }
  }
}
</script>

<style scoped>
.calendar-week {
  padding: 0;
  margin: 0;
  list-style: none;
  border-left: 1px solid #E4E7EA;
}

.week-item {
  box-sizing: border-box;
  float: left;
  width: 14.285%;
  height: 50px;
  border-right: 1px solid #E4E7EA;
  border-bottom: 1px solid #E4E7EA;
  cursor: pointer;
  text-align: center;
  line-height: 50px;
}
</style>