<template>
    <div id="map-container">
        <l-map :worldCopyJump="true" :maxBounds="bounds" :minZoom="2.3" :zoom="zoom" :center="center">
            <l-tile-layer :url="url"></l-tile-layer>
            <l-marker @mouseover="openPopup"
            :key="index"
            v-for="(mark, index) in markers"
            :lat-lng="latLng(mark.lat, mark.lng)"></l-marker>
        </l-map>
    </div>
</template>

<script>
import { LMap, LTileLayer, LMarker } from 'vue2-leaflet';
import L from 'leaflet';
import mockResponse from '../mockResponse.json';

export default {
    name: 'map-dashboard',
    props: [],
    components: {
     LMap, LTileLayer, LMarker 
    },
    computed : {
        markers() {
            return mockResponse;
        }
    },
    data() {
        return {
            zoom:2.3,
            center: L.latLng(0, 0),
            url:'https://tile.thunderforest.com/cycle/{z}/{x}/{y}.png?apikey=bbafaa3b53534ea0b7b19a553e22af1d',
            bounds : new L.LatLngBounds(new L.LatLng(89.99346179538875, 180), new L.LatLng(-89.98155760646617, -180)),
            msg: 'This is just a test data'
        }       
    },
    created : function() {
    },
    methods : {
        latLng : function(lat, lng) {
            return L.latLng(lat, lng);
        },
        openPopup : function(event) {
            event.target.bindTooltip(this.msg, {direction : 'top', permanent : false});
        }
    }
    
}
</script>
<style scoped>
#map-container {
    height: 95vh;
    width:100%;
}

</style>
