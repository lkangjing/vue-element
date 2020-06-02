<template>
  <div>
    <div style="width:800px;margin-left:50px">
      <Calendar ref="calendar" :events="events" @getCalendarEvents="getCalendarEvents" />
    </div>
  </div>
</template>

<script>
import Calendar from '@/components/calendar/Index'
export default {
  name: 'Rili',
  components: {
    // FullCalendar,
    Calendar
  },
  data() {
    return {
      events: [
        {
          start: '2020-6-05',
          //   end: '2019-12-09',
          content: '这是这件事的内容'
        },
        {
          start: '2020-5-08',
          end: '2020-5-10',
          content: '这是这件事的内容2'
        },
        {
          start: '2020-01-02',
          content: '这是哈哈哈'
        }
      ]
    }
  }
}
</script>

<style lang="scss">

</style>
