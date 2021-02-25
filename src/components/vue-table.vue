<template>
    <div class="vue-table">
      <div class="vue-table__header">
        <p>Name</p>
        <p>Points earned</p>
        <p>Points spent</p>
        <p>Registration date</p>
      </div>
      <div class="v-table__body">
        <vTableRow
            v-for="row in users_data"
            :key="row.id"
            :row_data="row"
        />
      </div>
    </div>
</template>

<script>
  import vTableRow from './v-table-row'
    export default {
        name: "vue-table",
      components: {
          vTableRow
      },
        props: {
          users_data: {
            type: Array,
            default: ()=> {
              return []
            }
          }
        }
    }
</script>

<style lang="scss" scoped>
  .vue-table {
    max-width: 900px;
    margin: 0 auto;
  }
  .vue-table__header {
    display: flex;
    justify-content: space-around;
    border-bottom: 1px solid #e7e7e7;
    p {
      flex-basis: 25%;
      text-align: left;
    }
  }
</style>