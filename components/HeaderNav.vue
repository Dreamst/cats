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

    border-radius: 10px;
    border: 1px solid #888888;
    cursor: pointer;
    &:not(:first-child) {
      margin-left: 30px;
    }
    a {
      padding: 8px 30px;
      display: block;
      text-decoration: none;

      &:visited {
        color: black;
      }
    }
  }
}

@media screen and (max-width: 460px) {
  .nav {
    &-container {
      height: auto;
      display: flex;
      justify-content: center;
      align-items: center;
      padding-top: 13px;
    }
    &-list {
      display: flex;
      flex-direction: column;
    }
    &-item {
      margin-bottom: 13px;
      &:last-child {
        margin-left: 0;
      }
    }
  }
}
</style>