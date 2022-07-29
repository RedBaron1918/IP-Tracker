<template>
  <div class="flex flex-col h-screen max-h-screen">
    <div
      class="z-20 flex justify-center bg-image-back bg-cover relative px-4 pt-8 pb-32"
    >
      <div class="w-full max-w-screen-sm">
        <h1 class="text-white text-center text-3xl pb-4">IP Tracker</h1>
        <div class="flex">
          <form @submit.prevent="getIPinfo" class="w-full h-full flex">
            <input
              class="flex-1 py-3 px-2 rounded-tl-md rounded-bl-md focus:outline-none"
              type="text"
              placeholder="Enter IP"
              v-model="Search"
            />
            <i
              class="fas fa-chevron-right cursor-pointer bg-black text-white px-4 rounded-tr-md rounded-br-md flex items-center"
              @click="getIPinfo"
            ></i>
          </form>
        </div>
      </div>
      <Info v-if="IPinfo" :IPinfo="IPinfo" />
    </div>

    <div id="map" class="h-full z-10"></div>
  </div>
</template>

<script>
import Info from "../components/Info.vue";
import Leaflet from "leaflet";
export default {
  name: "HomeView",
  components: { Info },
  data() {
    return {
      mymap: null,
      Search: "",
      IPinfo: null,
    };
  },
  methods: {
    async getIPinfo() {
      const data = await fetch(
        `https://geo.ipify.org/api/v2/country?apiKey=at_gopNAtLNayLEIV87wrOKAoWBhKeKe&ipAddress=${this.Search}`
      );
      const res = await data.json();
      this.IPinfo = {
        address: res.ip,
        state: res.location.region,
        timezone: res.location.timezone,
        isp: res.isp,
        // lat: res.location.lat,
        // lng: res.location.lng,
      };
      // Leaflet.marker([this.IPinfo.lat, this.IPinfo.lng]).addTo(map);
    },
  },
  mounted() {
    this.mymap = Leaflet.map("map").setView([51.505, -0.09], 13);

    Leaflet.tileLayer(
      "https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token=pk.eyJ1IjoicmVkYmFyb24xOTE4IiwiYSI6ImNsMGZieXkwZTA4anMzYnBnc3Vuank1NXEifQ.xzSuSwibaeP68W1ifW26IA",
      {
        attribution:
          'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
        maxZoom: 18,
        id: "mapbox/streets-v11",
        tileSize: 512,
        zoomOffset: -1,
        accessToken:
          "pk.eyJ1IjoicmVkYmFyb24xOTE4IiwiYSI6ImNsMGZieXkwZTA4anMzYnBnc3Vuank1NXEifQ.xzSuSwibaeP68W1ifW26IA",
      }
    ).addTo(this.mymap);
  },
};
</script>
