<template>
  <div class="Pagination">
    <div class="page-nav">
      <button @click="pageCounter > 0 ? pageCounter-- : false">Previous</button>
      <button
        @click="updateEvent(n + pageCounter)"
        v-for="n in buttonsToDisplay"
        :key="n"
        class="pageButton"
      >
        {{ n + pageCounter }}
      </button>
      <button v-on:click="counterNext()">Next</button>
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
        console.log(this.buttonNumber);
      } else {
        console.log(this.buttonNumber);
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

<style>
</style>