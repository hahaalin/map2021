<template>
  <div class="flex flex-col h-screen max-h-screen">
    <!-- Search / Results -->
    <div
      class="
        z-20
        flex
        justify-center
        relative
        bg-hero-pattern bg-cover
        px-4
        py-8
      "
    >
      <!-- Search Input -->
      <div class="w-full max-w-screen-sm">
        <h1 class="text-white text-center text-3xl pb-4">地理位置搜索</h1>
        <label class="block text-white">輸入IP地址以獲取地理位置信息。</label>
        <div class="flex">
          <input
            @keyup.enter="getIpInfo"
            v-model="queryIp"
            class="
              flex-1
              py-3
              px-2
              rounded-tl-md rounded-bl-md
              focus:outline-none
            "
            type="text"
            placeholder="例如159.117.76.247"
          />
          <div
            @click="getIpInfo"
            class="
              cursor-pointer
              bg-black
              text-white
              px-4
              rounded-tr-md rounded-br-md
              flex
              items-center
            "
          >
            <i class="fas fa-chevron-right"></i>
          </div>
        </div>
      </div>
      <!-- IP Info -->
      <IPInfo :parent-ipInfo="ipInfo" v-if="ipInfo"></IPInfo>
    </div>

    <!-- Map -->
    <div id="mapid" class="flex-1 z-10"></div>
  </div>
</template>

<script>
// @ is an alias to /src
import IPInfo from "@/components/IPInfo.vue";
import L from "leaflet";
import { onMounted, ref } from "vue";
import "leaflet/dist/leaflet.css";
import icon from "leaflet/dist/images/marker-icon.png";
import iconShadow from "leaflet/dist/images/marker-shadow.png";
import axios from "axios";
let DefaultIcon = L.icon({
  iconUrl: icon,
  shadowUrl: iconShadow,
});
L.Marker.prototype.options.icon = DefaultIcon;

export default {
  name: "Home",
  components: {
    IPInfo,
  },
  setup() {
    let mymap;
    let marker = null;
    // data

    const queryIp = ref("");
    const ipInfo = ref(null);

    onMounted(() => {
      mymap = L.map("mapid").setView([23.97565, 120.9738819], 8);
      marker = L.marker(["", ""]).addTo(mymap);
      L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
        attribution:
          '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
      }).addTo(mymap);

      getPosition();
    });

    const getPosition = () => {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(
          (position) => {
            console.log(position.coords.latitude, position.coords.longitude);

            marker
              .setLatLng([position.coords.latitude, position.coords.longitude])
              .bindPopup("你現在的位置在這邊")
              .openPopup();

            mymap.flyTo(
              [position.coords.latitude, position.coords.longitude],
              18
            );
          },
          (error) => {
            console.log(error.message);
          }
        );
      }
    };

    const getIpInfo = async () => {
      try {
        const response = await axios.get(
          `https://geo.ipify.org/api/v1?apiKey=at_FBTi0rGPhQlKp2cRdOJV0t3Mibq6F&ipAddress=${queryIp.value}`
        );
        const result = response.data;

        console.log(result);

        ipInfo.value = {
          address: result.ip,
          state: result.location.region,
          timezone: result.location.timezone,
          isp: result.isp,
          lat: result.location.lat,
          lng: result.location.lng,
        };

        marker
          .setLatLng([ipInfo.value.lat, ipInfo.value.lng])
          .bindPopup("你查詢的位置在這邊")
          .openPopup();

        mymap.flyTo([ipInfo.value.lat, ipInfo.value.lng], 18);
      } catch (err) {
        alert(err);
        queryIp.value = "";
      }
    };

    return { queryIp, ipInfo, getIpInfo, getPosition };
  },
};
</script>
<style lang="postcss">
.test {
  @apply text-2xl;
  height: calc(100vh - 12px);
}
</style>
