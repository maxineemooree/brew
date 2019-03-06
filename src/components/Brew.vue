<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <h1 class="text-center text-info">Breweries List</h1>
      </div>
      <!-- /.col-12 -->
    </div>
    <!-- /.row -->
    <div class="row">
      <div class="col-6">
        <BrewList @mouse-over-brew="mouseOverBrew" @mouse-left-brew="mouseLeftBrew" :brews="brews"/>
      </div>
      <!-- /.col-6 -->
      <div class="col-6">
        <BrewMap :brews="brews"/>
      </div>
      <!-- /.col-6 -->
    </div>
    <!-- /.row -->
  </div>
  <!-- /.container -->
</template>
<script>
import axios from "axios";
import BrewList from "./BrewList.vue";
import BrewMap from "./BrewMap";

export default {
  name: "Brew",
  components: {
    BrewList,
    BrewMap
  },

  data: function() {
    return {
      brews: [],
      normalIcon: [20, 20],
      largeIcon: [50, 50]
    };
  },
  mounted: function() {
    axios.get("https://api.openbrewerydb.org/breweries").then(r => {
      this.brews = r.data
        .filter(r => r.state == "Arizona")
        .map(r => {
          r.iconSize = this.normalIcon;
          return r;
        });
    });
  },
  methods: {
    mouseOverBrew: function(index) {
      this.brews[index].iconSize = this.largeIcon;
    },
    mouseLeftBrew: function(index) {
      this.brews[index].iconSize = this.normalIcon;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
</style>
