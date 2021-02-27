<template>
  <div class="vue-table">
    <div class="vue-table__header">
      <p @click="sortByName">Name <i class="material-icons">unfold_more</i></p>
      <p @click="sortByPointsEarned">Points earned <i class="material-icons">unfold_more</i></p>
      <p @click="sortByPointsEarned">Points spent <i class="material-icons">unfold_more</i></p>
      <p @click="sortByRegistrationDate">Registration date <i class="material-icons">unfold_more</i></p>
    </div>
    <div class="v-table__body">
      <vTableRow
          v-for="row in paginatedUsers"
          :key="row.id"
          :row_data="row"
      />
    </div>
    <div class="vue-table__pagination">
      <div class="prev" @click="prevClick">prev</div>
      <div class="page"
           v-for="(page, i) in pages"
           :kei="i"
           @click="pageClick(page)"
           :class="{'page__selected': page === pageNumber}"
      >
        {{page}}
      </div>
      <div class="next" @click="nextClick">next</div>
    </div>
  </div>
</template>

<script>
import vTableRow from './v-table-row'
import 'vue-material-design-icons/styles.css'
export default {
  name: "vue-table",
  components: {
    vTableRow
  },
  props: {
    users_data: {
      type: Array,
      default: () => {
        return []
      }
    }
  },
  data(){
    return {
      usersPerPage: 10,
      pageNumber: 1
    }
  },
  computed:{
    pages() {
      return Math.ceil(this.users_data.length / 10);
    },
    paginatedUsers() {
      let from = (this.pageNumber - 1) * this.usersPerPage;
      let to = from + this.usersPerPage;
      return this.users_data.slice(from, to)
    }
  },
  methods: {
    pageClick(page) {
      this.pageNumber = page;
    },
    prevClick() {
      if (this.pageNumber>0){
        this.pageNumber--;
        if ( this.pageNumber===0) {
          this.pageNumber+=1;
        }
      }
      else if (this.pageNumber<0) {
        return
      }
    },
    nextClick() {
      if (this.pageNumber>0){
        if (this.pageNumber===this.pages) {
          return
        }
        this.pageNumber++;
      }

    },
    sortByName() {
      this.users_data.sort((a,b)=> a.name.localeCompare(b.name))
    },
    sortByPointsEarned() {
      this.users_data.sort((a,b)=> a.points_earned - b.points_earned)
    },
    sortByPointsEarned() {
      this.users_data.sort((a,b)=> a.points_spent - b.points_spent)
    },
    sortByRegistrationDate() {
      this.users_data.sort((a,b)=> a.registration_date.localeCompare(b.registration_date))
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
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
.vue-table__pagination {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin-top: 30px;

  .page {
    padding: 5px;
    margin-right: 10px;
    border: 1px solid #e7e7e7;
    &:last-child {
      margin-right: 0;
    }
    &:hover {
      cursor: pointer;
      background: #aeaeae;
      color: white;
    }
  }
  .page__selected {
    background: #aeaeae;
    color: white;
  }
  .prev, .next {
    padding: 5px;
    border: 1px solid #e7e7e7;
    &:hover {
      cursor: pointer;
      background: #aeaeae;
      color: white;
    }
  }
  .prev {
    margin-right: 10px;
  }
}
</style>