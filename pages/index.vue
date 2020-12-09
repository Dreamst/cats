<template>
    <card-list> </card-list>
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
</style>
