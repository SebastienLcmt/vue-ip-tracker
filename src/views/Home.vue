<template>
  <div class="d-flex flex-column vh-100">
    <!--  Search / results -->
    <div class="position-relative z-index-header pt-4 pb-5 custom-gradient">
      <!-- Search input -->
      <div class="w-100 pb-3">
        <h1 class="fs-2 text-white text-center pb-4">IP Address Tracker</h1>
        <div class="row col-sm-12 col-md-8 col-lg-6 mx-auto pb-5">
          <div class="input-group">
            <input
              class="form-control shadow-none rounded-0 rounded-start"
              type="text"
              placeholder="Search for IP or leave empty to get your Ip info"
              v-model="queryIP"
            />
            <span type="button" @click="getIpInfo">
              <img
                src="../assets/chevron-right.svg"
                class="
                  input-group-text
                  rounded-0 rounded-end
                  bg-dark
                  border-0
                  h-100
                "
              />
            </span>
          </div>
        </div>
      </div>

      <!--  IP info -->
      <IPinfo v-if="ipData" :ipData="ipData"/>
    </div>
    <!-- Map -->
    <div id="map" class="h-100 z-index-map"></div>
  </div>
</template>

<script>
import IPinfo from '../components/IPinfo.vue'
import { onMounted, ref } from "vue";
import axios from "axios"
import leaflet from "leaflet";

export default {
  name: "Home",
  components: { IPinfo },
  setup() {
    let mymap;
    const queryIP = ref("");
    const ipData = ref(null);

    onMounted(() => {
      mymap = leaflet.map('map').setView([51.505, -0.09], 3);

      leaflet.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}', {
      attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
      maxZoom: 18,
      id: 'mapbox/streets-v11',
      tileSize: 512,
      zoomOffset: -1,
      accessToken: 'pk.eyJ1Ijoic2ViYXN0aWVubGNtdCIsImEiOiJjbDM2MnAxY3UweGFiM2dxc2VyamYwcjhlIn0.wjFbB-F-vsmUO-bga-K5-Q'}).addTo(mymap);
    })

    const getIpInfo = async () => {
      try {
        const data = await axios.get(`https://geo.ipify.org/api/v2/country,city,vpn?apiKey=at_QDm1NLWPjv8sNKJuVAcpKnUYv8jON&ipAddress=${queryIP.value}`)
        const result = data.data;       
        ipData.value = {
          address: result.ip,
          city: result.location.city,
          timezone: result.location.timezone,
          isp: result.isp,
          lat: result.location.lat,
          lng: result.location.lng,
        }
        leaflet.marker([ipData.value.lat, ipData.value.lng]).addTo(mymap);
        mymap.setView([ipData.value.lat, ipData.value.lng], 6)
      }
      catch(err){
        alert(err.message)
      }
    }

    return {
      queryIP,
      ipData,
      getIpInfo,
    }

  }
  
};
</script>

