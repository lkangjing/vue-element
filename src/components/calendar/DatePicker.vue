<template>
  <div class="calendar-body">
    <ul class="calendar-list clearfix">
      <date-item
        v-for="(dateItem, index) in calendarData"
        :key="index"
        :date="dateItem"
        :currentDate="currentDate"
        :index="index"
        @toggleEvent="toggle"
        :time="time">
      </date-item>
    </ul>
  </div>
</template>

<script>  
import DateItem from './DateItem'
export default {
  components: {
    DateItem
  },

  props: {
    calendarData: Array,
    currentDate: Object,
    time: Object
  },

  data () {
    return {
      
    }
  },

  methods: {
    toggle (state) {
    //   console.log(this.calendarData[state.index])
      this.calendarData[state.index].show = state.show
    },

    
  },
  
  
}
</script>

<style scoped>
.calendar-list {
  padding: 0;
  margin: 0;
  list-style: none;
  border-left: 1px solid #E4E7EA;
}

.clearfix:after {
  content: "";
  display: block;
  clear: both;
}
</style>