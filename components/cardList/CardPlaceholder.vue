<template>
  <div class="card">
    <div
      class="card-background"
    ></div>
    <div class="card-container">
      <div class="card-content">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardPlaceholder",
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
    animation-name: colorSwitch;
    animation-iteration-count:infinite;
    animation-direction: alternate;
    animation-duration: 1s;
    background-color: #e6e6e6;
    // @keyframes colorSwitch {
    //   0% {
    //     background-color: #e6e6e6;
    //   }
    //   100% {
    //     background-color: #cac8de;
    //   }
    // }
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