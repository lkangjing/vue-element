<template>
  <div class="calendar">
    <date-header :current-date="time" @handlerPrevMonth="handlerPrevMonth" @handlerNextMonth="handlerNextMonth"></date-header>
    <date-week></date-week>
    <date-picker 
      :calendarData="calendarData" 
      @sendCurrentDate="time = $event" 
      :events="events"
      :currentDate="currentDate"
      :time="time"></date-picker>
  </div>
</template>

<script>
import DatePicker from './DatePicker'
import DateHeader from './DateHeader'
import DateWeek from './DateWeek'
export default {
  data () {
    return {
      currentDate: null,
      calendarData: [],
      time: null
    }
  },

  props: {
    events: Array
  },

  components: {
    DateHeader,
    DatePicker,
    DateWeek
  }, 
  watch:{
      events(newName,oldName){
          console.log('events change');
          this.events = newName
          console.log(this.events);
          
      }
  },
  methods: {
    init (date) {
      console.log(date);
        
      const calendarData = []

      const dayTime = 24 * 60 * 60 * 1000
      // 获取当前年月日
      const {year, month, day} = this.getNewDate(date)
      this.time = {year, month, day}
      this.$emit('sendCurrentDate', this.currentDate)
      // 获取当月第一天日期   
      const currentFirstDay = this.getDate(year, month, 1)
      // 获取第一天是周几
      const weekDay = currentFirstDay.getDay()

      const startTime = currentFirstDay - weekDay * dayTime;
      // 循环生成35个日期
      for (let i = 0; i < 35; i++) {
        const date = new Date(startTime + i * dayTime)
        // 判断当前日期是否在事件范围内
        const events = this.events.filter(event => {
          const 
            start = new Date(new Date(event.start).toLocaleDateString()),
            end = event.end ? new Date(new Date(event.end).toLocaleDateString()) : start

            return start <= date && end >= date
        }).map(event => event.content)
        
        const {year, month, day} = this.getNewDate(date)
        const dateItem = {
          date: `${year}-${month}-${day}`,
          year, 
          month: month + 1, 
          day,
          events: events,
        }

        dateItem.events.length ? dateItem.show = false : null
        calendarData.push(dateItem)
      }      

    

      this.calendarData = calendarData
    },

    getNewDate (date) {
      let year = date.getFullYear();
      let month = date.getMonth();
      let day = date.getDate();
      return {year, month, day};
    }, 

    getDate (year, month, day) {
      return new Date(year, month, day);
    },

    handlerPrevMonth () {
      const date = new Date(this.time.year, this.time.month, this.time.day  )
      console.log(date)
      date.setMonth(this.time.month - 1)
      console.log(this.currentDate)
      this.$emit('getCalendarEvents',date)
      this.init(date)
    },

    handlerNextMonth () {
      const date = new Date(this.time.year, this.time.month, this.time.day  )
      date.setMonth(this.time.month + 1)
      this.init(date)
      console.log(this.currentDate)
      this.$emit('getCalendarEvents',date)

    }
  },

  created () {
    const {year, month, day} = this.getNewDate(new Date())
    this.currentDate = {year, month: month + 1, day}

    this.init(new Date())
    
  }
  
}
</script>

<style scoped>
.calendar {
  width: 100%;
}


</style>