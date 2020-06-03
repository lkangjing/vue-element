<template>
  <div>
    <div class="wrap">
      <div class="test" />
    </div>
    <button @click="start">动画</button>

    <div class="anniu" />
  </div>
</template>

<script>
export default {
  data() {
    return {

    }
  },
  methods: {
    start() {

    }
  }
}
</script>

<style lang="scss" scoped>
.wrap{
    width: 500px;
}
    .test{
        width: 10px;
        height: 175px;
        margin: 50px;
        // float: right;
        background: url("../../assets/404_images/arrow.jpg") no-repeat;
        // background-position: 100% 100%;
        // background: red;
    }
    .test:hover{
        width:373px;
        transition: width 3s linear;
        transform-origin: 100% 0;
    }
    .anniu{
        margin: 50px;
        width: 200px;
        height: 200px;
        border-radius: 44px;
        background: #71d7bf;
        box-shadow:  10px 10px 20px #458375,
             -10px -10px 20px #9dffff;
    }
</style>>

