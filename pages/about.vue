<template>
  <div class="container">
    <h1>About Cats App</h1>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: "About",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "About Cats App"
        }
      ]
    };
  }
};
</script>

<style scoped lang="scss">
.container {
  height: calc(100vh - 70px);
  display: flex;
  justify-content: center;
  align-items: flex-start;
  padding-top: 28px;
  h1 {
    padding: 10px;
    background: white;
    border: 1px solid grey;
    border-radius: 4px;
  }
}
</style>