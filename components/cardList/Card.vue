<template>
  <div class="card">
    <div
      class="card-background"
      :style="{ backgroundImage: 'url(' + imgURL +  ')' }"
    ></div>
    <div class="card-container">
      <div class="card-content">
        <p class="breed">{{breed}}</p>
        <p class="origin"></p>
        <a >Wikipedia</a>
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
        return "no info"
      }
      
    },
    imgURL() {
      if(this.data.hasOwnProperty("url")) {
          return this.data.url
      } else {
        return '';
      }
      
    },
  },
  methods: {},
  mounted() {
  }
};
</script>

<style scoped lang="scss">
.card {
  border-radius: 16px;
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
      background: #00000075;
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