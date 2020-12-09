<template>
  <div class="card">
    <div
      class="card-background"
      :style="{ backgroundImage: 'url(' + imgURL +  ')' }"
    ></div>
    <div class="card-container">
      <div class="card-content">
        <p class="breed">Breed: {{breed}}</p>
        <p class="origin">Origin: {{origin}}</p>
        <a v-if="wikiUrl" target="_blank" :href="wikiUrl" class="wiki">Wikipedia</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["data"],
  computed: {
    hasInfo() {
      if(this.data.breeds.length > 0) {
        return true
      } else {
        return false
        
      }
    },
    breed() {
      if(this.hasInfo) {
          return this.data.breeds[0].name
      } else {
        return "No breed info"
      }
      
    },
    imgURL() {
      if(this.data.hasOwnProperty("url")) {
          return this.data.url
      } else {
        return "./no_image.jpg";
      }
      
    },
    origin() {
      if(this.hasInfo ) {
        return this.data.breeds[0].origin
      } else {
        return "No origin info"
      }
    },
    wikiUrl() {
      if(this.hasInfo ) {
        return this.data.breeds[0].wikipedia_url
      } else {
        return false
      }
    },
  },
  mounted() {
  }
};
</script>

<style scoped lang="scss">
.card {
  border-radius: 6px;
  overflow: hidden;
  position: relative;
  height: 290px;
  .card-background {
    height: 290px;
    background-size: cover;
    background-position: center;
  }
  .card-container {
    height: 100%;
    position: absolute;
    width: 100%;
    top: 0;
    display: flex;
    align-items: flex-end;
    .card-content {
      display: flex;
      padding: 18px;
      align-items: center;
      flex-direction: column;
      background: linear-gradient(0deg, rgba(0,0,0,1) 0%, rgba(0,0,0,0.5354516806722689) 87%, rgba(255,255,255,0) 100%);
      width: 100%;
      p, a {
        color: white;
        text-decoration: none;
        margin: 10px 0;
      }
    }
  }
}


</style>