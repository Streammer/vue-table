<template>
  <div id="app">

  </div>
</template>

<script>
  import {mapActions, mapGetters} from 'vuex'
  export default {
    name : 'app',
    methods: {
      ...mapActions(['GET_USERS_FROM_API'])
    },
    computed: {
      ...mapGetters(['USERS'])
    },
    mounted(){
      this.GET_USERS_FROM_API()
    }
  }

</script>

<style lang="scss" scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

</style>
