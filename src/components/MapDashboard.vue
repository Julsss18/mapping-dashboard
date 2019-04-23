<template>
    <div id="map-container">
        <l-map @update:zoom="zoomUpdate" :maxBounds="bounds"  :maxZoom= "5" :minZoom="3" :zoom="zoom" :center="center">
            <l-tile-layer :attribution="attribution" :url="url"></l-tile-layer>
            <l-marker @mouseover="openPopup"
            :key="index"
            v-for="(mark, index) in markers"
            :lat-lng="latLng(mark.lat, mark.lng)">
                <l-icon :icon-url="markerIcon(mark)" :icon-size="iconSize"></l-icon>
            </l-marker>
        </l-map>
    </div>
</template>

<script>
import { LMap, LTileLayer, LMarker, LIcon } from 'vue2-leaflet';
import L from 'leaflet';
import mockResponse from '../mockResponse.json';
import greenIcon  from '../assets/green_icon.png';
import yellowIcon  from '../assets/yellow_icon.png';
import redIcon  from '../assets/red_icon.png';


export default {
    name: 'map-dashboard',
    props: [],
    components: {
     LMap, LTileLayer, LMarker, LIcon
    },
    computed : {
        markers() {
            return mockResponse;
        }
    },
    data() {
        return {
            zoom:2.75,
            center: L.latLng(40, 0),
            url:'http://{s}.tile.osm.org/{z}/{x}/{y}.png',
            attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
            currentZoom: 3,
            bounds : new L.LatLngBounds(new L.LatLng(89.99346179538875, 180), new L.LatLng(-89.98155760646617, -180)),
            msg: 'This is just a test data asdasdqwdqwdqd qwdqwdqwdqwdqw',
            iconSize: [30,30]
        }       
    },
    created : function() {
    },
    mounted : function() {
    },
    methods : {
        latLng : function(lat, lng) {
            return L.latLng(lat, lng);
        },
        openPopup : function(event) {
            let tooltip = L.tooltip({direction: 'top', permanent : false}).setContent(this.msg);
            event.target.bindTooltip(tooltip).openTooltip();
        },
        markerIcon : function(jsonData) {
            if (jsonData.errors > jsonData.threshold ) {
                return redIcon;
            } else if(jsonData.errors < jsonData.threshold && jsonData.errors < (jsonData.threshold/2)) {
                return greenIcon;
            } else {
                return yellowIcon;
            }
        },
        zoomUpdate : function(zoom) {
            if (this.currentZoom < zoom) {
                let size = [this.iconSize[0]+ 10, this.iconSize[1] + 10];
                this.iconSize = size;
            } else if (this.currentZoom > zoom) {
                if(this.iconSize[0] >20 && this.iconSize[1] > 20) {
                    let size = [this.iconSize[0]- 10, this.iconSize[1] - 10];
                    this.iconSize = size;
                }
            }
            this.currentZoom = zoom;
        }
    }
    
}
</script>
<style scoped>
#map-container {
    height: 98vh;
    width:100%;
}

.leaflet-container {
    font-size:22px!important;
}

</style>
