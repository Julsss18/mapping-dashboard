<template>
    <div id="map-container">
        <GmapMap :center="{lat:	16.416665, lng:120.5999976}"
                :zoom="7"
                map-type-id="roadmap"
                style="width: 100%; height: 600px">
                  <GmapMarker
                    :key="index"
                    v-for="(m, index) in markers"
                    :position="m.position"
                    :clickable="true"
                    :draggable="true"
                    @click="center=m.position"
                />
        </GmapMap>
    </div>
</template>
<script>
import { gmapApi } from 'vue2-google-maps';

export default {
    name: 'map-dashboard',
    props: [],
    computed: {
        google: gmapApi
    }
    
}
</script>
<style scoped>

</style>
