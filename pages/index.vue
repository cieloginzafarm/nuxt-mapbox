<template>
  <div>
    <script src="https://api.tiles.mapbox.com/mapbox.js/plugins/turf/v3.0.11/turf.min.js"></script>
    <script src="https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-draw/v1.2.0/mapbox-gl-draw.js"></script>
    <link
      rel="stylesheet"
      href="https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-draw/v1.2.0/mapbox-gl-draw.css"
      type="text/css"
    />
    <div id="map" @click="getCoordinates"></div>
    <div id="calculated-area"></div>
  </div>
</template>

<script>
import mapboxgl from "mapbox-gl";
export default {
  data() {
    return {
      map: {},
      coordinates: [],
      marker: null,
    };
  },
  mounted() {
    const mapboxgl = require("mapbox-gl");
    this.createMap();
    this.getCoordinates();
  },
  methods: {
    createMap() {
      mapboxgl.accessToken = this.access_token;
      this.map = new mapboxgl.Map({
        // accessToken: process.env.MAPBOX_TOKEN,
        accessToken:
          "pk.eyJ1IjoiY2llbG9naW56YWZhcm0iLCJhIjoiY2tnMGczbjIyMGQwMTJybGI4MGJsNTBzbSJ9.pPLT9Q2Kj_dUVW7BAqAyHw",
        container: "map",
        // style: process.env.MAPBOX_STYLE,
        style: "mapbox://styles/cieloginzafarm/ckg0gyibf04ld1aqds8wen9jh",
        center: [139.684363, 35.794831],
        zoom: 17,
      });

      this.draw = new MapboxDraw({
        displayControlsDefault: false,
        controls: {
          polygon: true,
          trash: true,
        },
      });
      this.map.addControl(this.draw);
    },
    getCoordinates() {
      self = this;
      this.map.on("click", function (e) {
        const currPos = JSON.parse(JSON.stringify(e.lngLat.wrap()));
        self.coordinates = [currPos["lng"], currPos["lat"]];
        if (self.marker != null) {
          self.marker.remove()
        }
        self.setCurrentMarker();
      });
    },
    setCurrentMarker() {
      this.marker = new mapboxgl.Marker()
        .setLngLat(this.coordinates)
        .addTo(this.map);
    },
  },
};
</script>

<style scoped>
#map {
  width: 100%;
  height: 100vh;
}
</style>
