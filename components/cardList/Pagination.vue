<template>
  <div class="Pagination">
    <div class="page-nav">
      <button class="previous" @click="pageCounter > 0 ? pageCounter-- : false">&lt;&lt;</button>
      <button
        @click="updateEvent(n + pageCounter)"
        v-for="n in buttonsToDisplay"
        :key="n"
        class="pageButton"
      >
        {{ n + pageCounter }}
      </button>
      <button class="next" v-on:click="counterNext()">&gt;&gt;</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Pagination",
  props: ["totalPage", "currentPage"],
  data() {
    return {
      pageCounter: 0,
      selectedPage: this.currentPage
    };
  },
  methods: {
    updateEvent(value) {
      this.selectedPage = value;
      this.$emit("update:currentPage", value);
    },
    counterNext() {
      if (this.pageCounter < this.totalPage - 9) {
        this.pageCounter++;
      } 
    }
  },
  computed: {
    buttonsToDisplay() {
      if (Number.isInteger(this.totalPage)) {
        if (this.totalPage < 10) {
          return this.totalPage;
        } else {
            return 10;
        }
      } else {
            return 10;
      }
    }
  },
  mounted() {
  }
};
</script>

<style lang="scss">
button {
    height: 30px;
    width: 30px;
    border: 1px solid white;
    background: white;
    cursor: pointer;
    &.previous, &.next {
        width: auto;
        padding: 0 20px
    }
}
</style>