<template>
<div>
    <div id="map" @click="getCoordinates"></div>
    <pre>{{ wayPoints }}</pre>
</div>
</template>

<script>
import mapboxgl from 'mapbox-gl'
export default {
    data() {
        return {
            access_token: "pk.eyJ1IjoiY2llbG9naW56YWZhcm0iLCJhIjoiY2tnMGczbjIyMGQwMTJybGI4MGJsNTBzbSJ9.pPLT9Q2Kj_dUVW7BAqAyHw",
            map: {},
            wayPoints: "",
        }
    },
    mounted() {
        this.createMap()
        this.getCoordinates()
    },
    methods: {
        createMap() {
            mapboxgl.accessToken = this.access_token
            this.map = new mapboxgl.Map({
                container: 'map',
                style: 'mapbox://styles/cieloginzafarm/ckg0gyibf04ld1aqds8wen9jh',
                center: [139.684363, 35.794831],
                zoom: 17
            })
        },
        getCoordinates() {
            self = this
            this.map.on('mousedown', function (e) {
                self.wayPoints = JSON.stringify(e.lngLat.wrap());
            });
            console.log(this.wayPoints)

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
