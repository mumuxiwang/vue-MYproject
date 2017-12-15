<template>
  <div id="app">
    <div class="wm" @click="handleClick">{{massage}}</div>
  </div>
</template>

<script>
  export default {
    name: 'app',
    data () {
      return {
        massage: 'hello world'
      }
    },
    methods: {
      handleClick () {
        this.massage = 'bye world'
      }
    }
}
</script>

<style scoped>
  .wm {
    color:green;
  }
</style>
