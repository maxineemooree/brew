<template>
  <div class="row map">
    <!-- <h2>Center is {{currentCenter}} , zoom is {{currentZoom}}</h2> -->
    <l-map @update:zoom="zoomUpdate" @update:center="centerUpdate" :zoom="zoom" :center="center">
      <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
      <l-marker
        :key="index"
        v-for="(brew, index) in brews"
        :lat-lng="latLng(brew.latitude, brew.longitude)"
      >
        <l-icon :icon-size="brew.iconSize" :icon-url="icon"></l-icon>
      </l-marker>
    </l-map>
  </div>
  <!-- /.row map -->
</template>
<script>
import { LMap, LTileLayer, LMarker, LIcon } from "vue2-leaflet";
import beer from "../assets/beer.png";

export default {
  name: "BrewMap",
  props: {
    brews: Array
  },
  data: function() {
    return {
      zoom: 6,
      center: L.latLng(33.750321, -112.694836),
      currentCenter: L.latLng(33.750321, -112.694836),
      currentZoom: 6,
      url:
        "https://tile.thunderforest.com/transport/{z}/{x}/{y}.png?apikey=0047fe40789d4f248a277a3bf7e5bdd4",
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      marker: L.latLng(47.41322, -1.219482),
      icon: beer,
      iconSize: [20, 20]
    };
  },
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LIcon
  },
  methods: {
    latLng: function(lat, lng) {
      return L.latLng(lat, lng);
    },
    centerUpdate: function(center) {
      this.currentCenter = center;
    },
    zoomUpdate: function(zoom) {
      this.currentZoom = zoom;
    }
  }
};
</script>
<style lang="scss" scoped>
.map {
  height: 95vh;
}
</style>
