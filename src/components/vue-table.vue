<template>
  <div class="vue-table">
    <div class="vue-table__header">
      <p @click="sortByName">Name <svg xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 0 24 24" width="24"><path d="M0 0h24v24H0z" fill="none"/><path d="M3 18h6v-2H3v2zM3 6v2h18V6H3zm0 7h12v-2H3v2z"/></svg></p>
      <p @click="sortByPointsEarned">Points earned <svg xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 0 24 24" width="24"><path d="M0 0h24v24H0z" fill="none"/><path d="M3 18h6v-2H3v2zM3 6v2h18V6H3zm0 7h12v-2H3v2z"/></svg></p>
      <p @click="sortByPointsEarned">Points spent <svg xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 0 24 24" width="24"><path d="M0 0h24v24H0z" fill="none"/><path d="M3 18h6v-2H3v2zM3 6v2h18V6H3zm0 7h12v-2H3v2z"/></svg></p>
      <p @click="sortByRegistrationDate">Registration date <svg xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 0 24 24" width="24"><path d="M0 0h24v24H0z" fill="none"/><path d="M3 18h6v-2H3v2zM3 6v2h18V6H3zm0 7h12v-2H3v2z"/></svg></p>
    </div>
    <div class="v-table__body">
      <vTableRow
          v-for="row in paginatedUsers"
          :key="row.id"
          :row_data="row"
      />
    </div>
    <div class="vue-table__pagination">
      <div class="prev" @click="prevClick" v-show="showLeft">prev</div>
      <div class="page"
           v-for="(page, i) in pages"
           :kei="i"
           @click="pageClick(page)"
           :class="{'page__selected': page === pageNumber}"
      >
        {{page}}
      </div>
      <div class="next" @click="nextClick" v-show="showRight">next</div>
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
      default: () => {
        return []
      }
    }
  },
  data(){
    return {
      usersPerPage: 10,
      pageNumber: 1,
      showLeft: true,
      showRight: true
    }
  },
  computed:{
    pages() {
      return Math.ceil(this.users_data.length / this.usersPerPage);
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
      this.showControls();
      console.log(this.pageNumber)
    },
    prevClick() {
      if (this.pageNumber>0){
        this.pageNumber--;
        this.showControls()
        if ( this.pageNumber===0) {
          this.pageNumber=1;
        }
        this.showControls()
      }
      else if (this.pageNumber<0) {
        return
      }
      this.showControls()
    },
    nextClick() {

      if (this.pageNumber>0){
        if (this.pageNumber===this.pages) {
          return
        }
        this.pageNumber++;
      }
      this.showControls()
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
    },
    showControls() {
      if(this.pageNumber === 1) {
         this.showLeft = false
      }
      if(this.pageNumber === Math.ceil(this.users_data.length / this.usersPerPage)) {
         this.showRight = false
      }
      if (this.pageNumber < 1) {
        this.showLeft = true
      }
      if (this.pageNumber < Math.ceil(this.users_data.length / this.usersPerPage)) {
        this.showRight = true
      }
      if (this.pageNumber > 1) {
        this.showLeft = true
      }
      else {
        return
      }
    }
  },
  mounted() {
    this.showControls()
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