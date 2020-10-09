<template>
<div>
    <div id="map" @click="getCoordinates"></div>
</div>
</template>

<script>
import mapboxgl from 'mapbox-gl'
export default {
    data() {
        return {
            map: {},
            coordinates: [],
            marker: null,
        }
    },
    mounted() {
        const mapboxgl = require('mapbox-gl')
        this.createMap()
        this.getCoordinates()
    },
    methods: {
        createMap() {
            mapboxgl.accessToken = this.access_token
            this.map = new mapboxgl.Map({
                // accessToken: process.env.MAPBOX_TOKEN,
                accessToken: "pk.eyJ1IjoiY2llbG9naW56YWZhcm0iLCJhIjoiY2tnMGczbjIyMGQwMTJybGI4MGJsNTBzbSJ9.pPLT9Q2Kj_dUVW7BAqAyHw",
                container: 'map',
                // style: process.env.MAPBOX_STYLE,
                style: "mapbox://styles/cieloginzafarm/ckg0gyibf04ld1aqds8wen9jh",
                center: [139.684363, 35.794831],
                zoom: 17
            })

            this.marker = new mapboxgl.Marker()
                .setLngLat([139.684363, 35.794831])
                .addTo(this.map);
        },
        getCoordinates() {
            self = this
            this.map.on('click', function (e) {
                const currPos = JSON.parse(JSON.stringify(e.lngLat.wrap()))
                self.coordinates = [currPos['lng'], currPos['lat']]
                self.addMarker()
            });
        },
        addMarker() {
            this.marker = new mapboxgl.Marker()
                .setLngLat(this.coordinates)
                .addTo(this.map);
        }
    }
}
</script>

<style scoped>
#map {
    width: 100%;
    height: 100vh;
}
</style>
