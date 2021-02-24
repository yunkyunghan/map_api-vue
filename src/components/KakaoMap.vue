<template>
  <div>
   <h1>Daum Map Demo</h1>
   <button @click="drawMarkers">Draw Markers</button>
   <button @click="drawDirection">Draw Direction</button>
   <button @click="clearMap">Clear Map</button>
    <vue-daum-map
      :appKey="appKey"
      :center.sync="center"
      :level.sync="level"
      :mapTypeId="mapTypeId"
      :libraries="libraries"

      @load="onLoad"
      @center_changed="onMapEvent('center_changed', $event)"
      @zoom_start="onMapEvent('zoom_start', $event)"
      @zoom_changed="onMapEvent('zoom_changed', $event)"
      @bounds_changed="onMapEvent('bounds_changed', $event)"
      @click="onMapEvent('click', $event)"
      @dblclick="onMapEvent('dblclick', $event)"
      @rightclick="onMapEvent('rightclick', $event)"
      @mousemove="onMapEvent('mousemove', $event)"
      @dragstart="onMapEvent('dragstart', $event)"
      @drag="onMapEvent('drag', $event)"
      @dragend="onMapEvent('dragend', $event)"
      @idle="onMapEvent('idle', $event)"
      @tilesloaded="onMapEvent('tilesloaded', $event)"
      @maptypeid_changed="onMapEvent('maptypeid_changed', $event)"

      style="width:100%;height:500px;">
    </vue-daum-map>

    <h2>Options</h2>
    <table>
      <colgroup>
        <col width="60" />
        <col />
      </colgroup>
      <tr>
        <th>Level</th>
        <td><input type="range" min="1" max="14" v-model.number="level"> {{level}}</td>
      </tr>
      <tr>
        <th>Lat</th>
        <td><input type="number" v-model.number="center.lat" step="0.0001"></td>
      </tr>
      <tr>
        <th>Lng</th>
        <td><input type="number" v-model.number="center.lng" step="0.0001"></td>
      </tr>
    </table>  
  </div>
</template>

<script>
/* global kakao */
import VueDaumMap from 'vue-daum-map';
//const markers = []
const home ={lat:37.55532937435788, lng:127.15405767072278};
const work ={lat:37.48563184556581, lng:127.01634362354709};
export default {
    name: 'KakaoMap',

    components: {
      VueDaumMap
      },

    data: () => ({
      appKey: "cf22b457420393c7c19d1db0d5f86e67",
      center: home,
      level: 3,
      mapTypeId: VueDaumMap.MapTypeId.NORMAL,
      libraries: [],
      map: null,
    }),

    makers: [],

    methods: {
      onLoad (map) {
      this.map = map;
      
      },
      onMapEvent (event ,params) {
      if(event == 'click') {
            var marker = new kakao.maps.Marker({
            position : new kakao.maps.LatLng(params['0']["latLng"]['Ma'],params['0']["latLng"]['La']),
          
      })
      marker.setMap(this.map)
      // markers.push(marker)
      // for (var i = 0 ; i < markers.length; i++){
      //   if (i == makers.length-1){
      //     markers[i].setMap(this.map)
      //   }
      //   else{
      //     markers[i].setMap(null)
      //   }
      // }

      
    }
       
      },

      drawMarkers(){
        this.marker = [
          {
            map: this.map,
            position : home,
          },
          {
            position: work,
          }
        ];
      },
      drawDirection(){
        alert("drawDirection");
      },
      clearMap(){
        alert("clearMap");
      }
    }
    };
</script>