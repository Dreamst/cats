<template>
  <div class="CardList">
    <h1>CardList</h1>
    <pagination
      v-on:update:currentPage="updatePage"
      :totalPage="totalPage"
      :currentPage.sync="currentPage"
    ></pagination>
    <div class="cards-container" v-if="data.length > 0">
      <card v-for="item in data" :data="item" :key="item.id"> </card>
    </div>
  </div>
</template>

<script>
import Pagination from "@/components/cardList/Pagination";
import Card from "@/components/cardList/Card";

export default {
  name: "CardList",
  components: {
    Pagination,
    Card
  },
  data() {
    return {
      data: {},
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
        `https://api.thecatapi.com/v1/images/search?limit=${pageLimit}&page=${page}&order=Desc`,
        {
          method: "GET",
          headers: {
            "x-api-key": "0942a7cb-ed6c-42b4-a645-d6af589f2119"
          }
        }
      );

      const data = await res.json();
      for (let entry of res.headers.entries()) {
        if (entry[0] == "pagination-count") {
          this.totalItems = parseInt(entry[1]);
        }
      }
      this.data = data;
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
.CardList {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.cards-container {
  display: grid;
  grid-template-columns: repeat(4, 200px);
  grid-gap: 40px;
  margin: auto;
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