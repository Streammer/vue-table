<template>
  <div id="app">
    <vTable
        :users_data="USERS"
    />
  </div>
</template>

<script>
  import {mapActions, mapGetters} from 'vuex'
  import vTable from '@/components/vue-table'
  export default {
    name : 'app',
    components: {vTable},
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
