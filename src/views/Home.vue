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
        pt-8
        pb-32
      "
    >
      <!-- Search Input -->
      <div class="w-full max-w-screen-sm">
        <h1 class="text-white text-center text-3xl pb-4">IP Address Tracker</h1>
        <div class="flex">
          <input
            v-model="queryIp"
            class="
              flex-1
              py-3
              px-2
              rounded-tl-md rounded-bl-md
              focus:outline-none
            "
            type="text"
            placeholder="Search for any IP address or leave empty to get your ip info"
          />
          <div
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
      <IPInfo></IPInfo>
    </div>

    <!-- Map -->
    <div id="mapid" class="h-full z-10"></div>
  </div>

  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>

  <div class="flex justify-evenly p-10 focus-within:bg-green-100 group">
    <box
      class="
        bg-red-500
        hover:bg-red-400
        ring-red-300
        focus:ring-4
        group-hover:text-gray-600
        font-bold
        flex
        justify-center
        items-center
        rounded-md
        cursor-pointer
        outline-none
        w-20
        h-20
        text-3xl text-white
      "
      tabindex="0"
    >
      1
    </box>
    <box
      class="
        bg-blue-500
        hover:bg-blue-400
        ring-blue-300
        focus:ring-4
        group-hover:text-gray-600
        font-bold
        flex
        justify-center
        items-center
        rounded-md
        cursor-pointer
        outline-none
        w-20
        h-20
        text-3xl text-white
      "
      tabindex="1"
    >
      2
    </box>
  </div>
</template>

<style></style>
<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import IPInfo from "@/components/IPInfo.vue";
import L from "leaflet";
import { onMounted, ref } from "vue";
import "leaflet/dist/leaflet.css";

export default {
  name: "Home",
  components: {
    HelloWorld,
    IPInfo,
  },
  setup() {
    let mymap;
    // data

    onMounted(() => {
      mymap = L.map("mapid").setView([22.604799, 120.2976256], 13);

      L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
        attribution:
          '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
      }).addTo(mymap);
    });
  },
};
</script>
<style lang="postcss">
.test {
  @apply text-2xl;
  height: calc(100vh - 12px);
}
</style>
