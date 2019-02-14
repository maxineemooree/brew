<template>
  <div class="card brew-list">
    <ul class="list-group list-group-flush">
      <li
        v-bind:key="index"
        v-for="(brew, index) in brews"
        class="list-group-item"
      >{{brew.name}}, {{brew.state}}</li>
    </ul>
  </div>
</template>
<script>
export default {
  name: "BrewList",
  props: {
    brews: Array
  }
};
</script>
<style lang="scss" scoped>
.brew-list {
  overflow-y: scroll;
  height: 96vh;
  li {
    &:hover {
      background-color: darkgrey;
    }
  }
}
</style>

