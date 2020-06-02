<template>
  <li 
    :class="[
      'calendar-item', 
      {'not-current-month': notCurrentMonth}, 
      {'already-day': isAlready}
    ]"
    
    @mouseenter="toggleEvent(true)"
    @mouseleave="toggleEvent(false)">
      <i v-if="date.events.length" class="event-dot"></i>
      {{date.day}}
      <transition name="toggle">
        <div class="event-card" v-if="date.show">
          <p v-for="(event, index) in date.events" :key="index">{{event}}</p>
        </div>
      </transition>
    </li>
</template>

<script>
export default {
  props: {
    date: Object,
    currentDate: Object,
    index: Number,
    time: Object
  },

  computed: {
    notCurrentMonth () {
      // console.log(this.date.month, this.time.month + 1)
      return this.date.month !== this.time.month + 1 || this.date.year !== this.time.year
    },

    isCurrentDay () {
      return this.date.day === this.currentDate.day && this.date.month === this.currentDate.month && this.date.year === this.currentDate.year
    },

    isAlready () {
      const current = new Date(`${this.date.year}-${this.date.month}-${this.date.day}`)
      const date = new Date(`${this.currentDate.year}-${this.currentDate.month}-${this.currentDate.day}`)
      return date >= current && !this.notCurrentMonth
    }
  },
  
  methods: {
    toggleEvent (status) {
      if (this.date.events.length) {
        this.$emit('toggleEvent', {show: status, index: this.index})
      }
    }
  }
}
</script>

<style scoped>
.calendar-item {
  box-sizing: border-box;
  float: left;
  width: 14.285%;
  height: 65px;
  border-right: 1px solid #E4E7EA;
  border-bottom: 1px solid #E4E7EA;
  cursor: pointer;
  padding: 10px;
  color: #333;
  position: relative;
}

.already-day {
  background: #ffff99;
  color: #000;
}

.not-current-month {
  background-image: linear-gradient(45deg,rgba(000, 000, 000, .03) 25%,transparent 25%,transparent 50%,rgba(000, 000, 000, .03) 50%,rgba(000, 000, 000, .03) 75%,transparent 75%,transparent);
  background-size: 20px 20px;
  cursor: not-allowed;
  color: #aaa;
}

.event-dot {
  position: absolute;
  right: 10px;
  top: 10px;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: #009ad8;
  box-shadow: 0 0 5px 0px #009ad8;
  border: 1px solid rgba(255,255,255,.9);
}
.event-card {
    position: absolute;
    z-index: 99;
    background-color: rgba(255, 255, 255, .8);
    border-radius: 10px;
    padding: 10px;
    font-size: 14px;
    width: 200%;
}

.toggle-enter, .toggle-leave-to {
  opacity: 0;
}

.toggle-enter-to, .toggle-leave {
  opacity: 1;
}

.toggle-enter-active, .toggle-leave-avtive {
  transition: all 1s;
}
</style>