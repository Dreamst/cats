<template>
  <div class="nav-container">
    <ul class="nav-list">
      <li class="nav-item">
        <nuxt-link to="/">Home</nuxt-link>
      </li>
      <li class="nav-item">
        <nuxt-link to="/about">About</nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "HeaderNav"
};
</script>

<style scoped lang="scss">
.nav {
  &-container {
    max-width: 1400px;
    margin: auto;
    background: #98a5bd;
    height: 70px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  &-list {
    list-style-type: none;
    padding-left: 0;
  }
  &-item {
    display: inline-block;
    background: white;
    padding: 8px 30px;
    border-radius: 10px;
    &:not(:first-child) {
      margin-left: 30px;
    }
    a {
      text-decoration: none;
      &:visited {
        color: black;
      }
    }
  }
}
</style>