<template>
  <div class="CardList">
    <h1 class="title">Cat List</h1>
    <transition name="fade">
    <pagination
      v-if="dataExists"
      v-on:update:currentPage="updatePage"
      :totalPage="totalPage"
      :currentPage.sync="currentPage"
      ref="pagination"
    ></pagination>
    </transition>
    <category-select v-if="dataExists" @categoryUpdated="categoryUpdate($event)"></category-select>
    <div v-else class="empty"></div>
    <div v-if="$fetchState.pending">
      <p class="texte-placeholder">Récupération des chats</p>
      <div class="cards-container">
      <card-placeholder
        v-for="item in itemPerPage"
        :key="item"
      ></card-placeholder>
    </div>
    </div>
    
    <div class="cards-container" v-else-if="dataExists"> 
      <card v-for="item in catData" :data="item" :key="item.id"></card>
    </div>
    
  </div>
</template>

<script>
import Pagination from "@/components/cardList/Pagination";
import Card from "@/components/cardList/Card";
import CardPlaceholder from "@/components/cardList/CardPlaceholder";
import CategorySelect from "@/components/cardList/CategorySelect";

export default {
  name: "CardList",
  components: {
    Pagination,
    Card,
    CategorySelect,
  },
  data() {
    return {
      catData: {},
      totalItems: undefined,
      itemPerPage: 12,
      currentPage: 1,
      category: '',

    };
  },
  async fetch() {
    let pageLimit = this.itemPerPage;
    let page = this.currentPage;
    let category = this.category;
    let res = await fetch(
        `https://api.thecatapi.com/v1/images/search?limit=${pageLimit}&page=${page - 1}&order=Desc${category}`,
        {
          method: "GET",
          headers: {
            "x-api-key": "0942a7cb-ed6c-42b4-a645-d6af589f2119"
          }
        }
      );
      console.log("fetching");
      const catData = await res.json();
      //Get
      for (let entry of res.headers.entries()) {
        if (entry[0] == "pagination-count") {
          this.totalItems = parseInt(entry[1]);
        }
      }
      this.catData = catData;
  },
  // 
  computed: {
    dataExists() {
      return this.catData.length > 0;
    },
    totalPage() {
      if (Number.isInteger(this.totalItems / this.itemPerPage)) {
        return this.totalItems / this.itemPerPage - 1;
      } else {
        return Math.floor(this.totalItems / this.itemPerPage);
      }
    }
  },
  methods: {
    
    updatePage(page) {
      this.currentPage = page;
      this.$fetch();
    },
    categoryUpdate(value) {
      this.$refs.pagination.pageCounter = 0;
      this.currentPage = 1;
      let categoryQuery;
      if(value.length > 2) {
        categoryQuery = `&breed_ids=${value}`
        this.category = categoryQuery;
      } else if (value != '') {
        categoryQuery = `&category_ids=${value}`
        this.category = categoryQuery;
      } else {
        categoryQuery = '';
        this.category = categoryQuery;
      }
      this.$fetch();
    }
  },
  mounted() {
  }
};
</script>

<style scoped lang="scss">
.title {
  padding: 10px;
  background: white;
  border: 1px solid grey;
  border-radius: 4px;
  margin: 28px 0;
  text-align: center;
}
.empty {
  height: 87px;
}
.CardList {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 0 0 40px;
}
.cards-container {
  display: grid;
  grid-template-columns: repeat(4, 200px);
  grid-gap: 40px;
  margin: auto;
  margin-top: 28px;
}
@media screen and (max-width: 1010px) {
  .cards-container {
    grid-template-columns: repeat(3, 200px);
    grid-gap: 30px;
  }
}
@media screen and (max-width: 730px) {
  .cards-container {
    grid-template-columns: repeat(2, 200px);
  }
}
@media screen and (max-width: 500px) {
  .cards-container {
    grid-template-columns: repeat(1, 200px);
  }
}

// transition 

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>