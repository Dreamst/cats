<template>
  <select @change="categoryUpdated($event)" name="category">
    <option value="">--Please choose a category--</option>
    <option value="1">Hats</option>
    <option value="2">Space</option>
    <option value="3">Gifs</option>
    <option value="4">Glasses</option>
    <option value="5">Boxes</option>
    <option value="beng">Bengal</option>
  </select>
</template>

<script>
export default {
  name: "CategorySelect",
  methods: {
    categoryUpdated(event) {
      this.$emit("categoryUpdated", event.target.value);
    }
  }
};
</script>

<style>
select {
  padding: 10px 10px;
  margin: 20px 0 4px;
  border: none;
  display: grid;
}
select:not(:-internal-list-box) {
  overflow: visible;
}
select::after {
  content: "";
  width: 0.8em;
  height: 0.5em;
  background-color: blue;
  clip-path: polygon(100% 0%, 0 0%, 50% 100%);
}

</style>