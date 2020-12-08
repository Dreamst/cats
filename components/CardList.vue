<template>
  <div class="CardList">
    <h1>CardList</h1>
    <button>OK</button>
    <pagination></pagination>
    <div class="cards-container">
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
      data: null,
    };
  },
  methods: {
    test() {
      console.log("test");
    },
    async fetchApi(limit = 5, page = 1) {
      let res = await fetch(
        `https://api.thecatapi.com/v1/images/search?limit=${limit}&page=${page}&order=Desc&breed_ids=beng`
      );
      const data = await res.json();
      this.data = data;
    },
    initData() {}
  },
  mounted() {
    this.fetchApi();
  }
};
</script>

<style scoped lang="scss">
.cards-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
</style>