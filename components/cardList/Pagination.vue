<template>
  <div class="Pagination">
    <div class="page-nav">
      <button class="previous-nav" @click="pageCounter > 0 ? pageCounter-- : false">&lt;&lt;</button>
      <button class="previous" @click="selectedPage > 1 ? updateEvent(selectedPage - 1): false">Previous</button>
      <button
        @click="updateEvent(n + pageCounter)"
        :class="{highlight: n + pageCounter == selectedPage}"
        v-for="n in buttonsToDisplay"
        :key="n"
        class="pageButton"
      >
        {{ n + pageCounter }}
      </button>
      <button class="next" @click="selectedPage < totalPage ? updateEvent(selectedPage + 1): false">Next</button>
      <button class="next-nav" v-on:click="counterNext()">&gt;&gt;</button>
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
    selectedPage() {
      return this.currentPage;
    },
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
};
</script>

<style lang="scss">
.page-nav {
  display:flex;
  flex-wrap: wrap;
  button {
    height: 30px;
    width: 30px;
    border: 1px solid white;
    background: white;
    cursor: pointer;
    margin-left: 10px;
    margin-bottom: 10px;
    &:focus {
      outline: none;
    }
    &.highlight {
      border: 2px solid grey;
    }
    &.next, &.previous, &.previous-nav, &.next-nav {
        width: auto;
        padding: 0 20px
    }
}
}

</style>