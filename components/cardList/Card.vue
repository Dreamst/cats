<template>
  <div class="card">
    <div class="background-container" :stlye="{BackgroundImage: imgURL}" >

    </div>
      
      {{name}}
      {{imgURL}}
      {{wikiLink}}
  </div>
</template>

<script>
export default {
    name: "Card",
    props: ["name","imgURL", "wikiLink", "origin"],
    computed: {

    },
    methods: {
    },
    mounted() {
    }

}
</script>

<style scoped lang="scss">
.card {
  width: 100%;
}
.background-container {
  height: 100px;
}
</style>