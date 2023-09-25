<template>
  <div  class=" w-full h-72 text-center mb-6 z-0">
    <l-map class="z-0" :useGlobalLeaflet="false" ref="map" v-model:zoom="zoom" :center="[47.41322, -1.219482]">
      <l-tile-layer url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png" layer-type="base"
        name="OpenStreetMap"></l-tile-layer>
    </l-map>
  </div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import { LMap, LTileLayer } from "@vue-leaflet/vue-leaflet";

export default {
  components: {
    LMap,
    LTileLayer,
  },
  data() {
    return {
      zoom: 2,
    };
  },
};
</script>

<style></style>