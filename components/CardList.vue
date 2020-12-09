<template>
  <div class="CardList">
    <h1 class="title">Cat List</h1>
    <pagination
      v-if="catData.length > 0"
      v-on:update:currentPage="updatePage"
      :totalPage="totalPage"
      :currentPage.sync="currentPage"
    ></pagination>
    <div v-else class="empty"></div>

    <div class="cards-container" v-if="catData.length > 0">
      <card v-for="item in catData" :data="item" :key="item.id"> </card>
    </div>
    <div class="cards-container" v-else>
      <card-placeholder
        v-for="item in itemPerPage"
        :key="item"
      ></card-placeholder>
    </div>
  </div>
</template>

<script>
import Pagination from "@/components/cardList/Pagination";
import Card from "@/components/cardList/Card";
import CardPlaceholder from "@/components/cardList/CardPlaceholder";

export default {
  name: "CardList",
  components: {
    Pagination,
    Card
  },
  data() {
    return {
      catData: {},
      totalItems: undefined,
      itemPerPage: 12,
      currentPage: 1
    };
  },
  computed: {
    totalPage() {
      if (Number.isInteger(this.totalItems / this.itemPerPage)) {
        return this.totalItems / this.itemPerPage - 1;
      } else {
        return Math.floor(this.totalItems / this.itemPerPage);
      }
    }
  },
  methods: {
    async fetchApi(pageLimit, page) {
      let res = await fetch(
        `https://api.thecatapi.com/v1/images/search?limit=${pageLimit}&page=${page - 1}&order=Desc&category_ids=1`,
        {
          method: "GET",
          headers: {
            "x-api-key": "0942a7cb-ed6c-42b4-a645-d6af589f2119"
          }
        }
      );

      const catData = await res.json();
      //Get
      for (let entry of res.headers.entries()) {
        if (entry[0] == "pagination-count") {
          this.totalItems = parseInt(entry[1]);
        }
      }
      this.catData = catData;
    },
    updatePage(page) {
      this.currentPage = page;
      this.fetchApi(this.itemPerPage, this.currentPage);
    }
  },
  mounted() {
    this.fetchApi(this.itemPerPage, this.currentPage);
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
  height: 30px;
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
</style>