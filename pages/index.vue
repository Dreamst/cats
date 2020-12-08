<template>
  <div class="container">
    <card-list> </card-list>
  </div>
</template>

<script>

import CardList from "@/components/CardList";

export default {
  head() {
    return {
      title: "Cats App",
      meta: [ {
        hid: "description",
        name: "description",
        content: "A comprehensive listing of cats",
      }],
    }
  },
  components: {
    CardList,
  }
}
</script>

<style scoped lang="scss">
  .container {
    max-width: 1400px;
    margin: auto;
  }
</style>
