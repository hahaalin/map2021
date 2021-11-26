<template>
  <div
    class="
      absolute
      top-full
      flex flex-col
      lg:flex-row
      bg-white
      gap-y-4 gap-x-12
      px-8
      pt-8
      pb-12
      rounded-md
    "
  >
    <!-- Flex Item #1  -->
    <div class="flex flex-col">
      <h3 class="text-xs mb-2 uppercase">IP地址</h3>
      <span class="text-2xl">{{ parentIpInfo.address }}</span>
    </div>
    <!-- Flex Item #2  -->
    <div class="flex flex-col">
      <h3 class="text-xs mb-2 uppercase">國家</h3>
      <span class="text-2xl">{{ parentIpInfo.state }}</span>
    </div>
    <!-- Flex Item #3  -->
    <div class="flex flex-col">
      <h3 class="text-xs mb-2 uppercase">時區</h3>
      <span class="text-2xl">UTC {{ parentIpInfo.timezone }}</span>
    </div>
    <!-- Flex Item #4  -->
    <div class="flex flex-col">
      <h3 class="text-xs mb-2 uppercase">服務供應商</h3>
      <span class="text-2xl capitalize">{{ parentIpInfo.isp }}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: ["parent-ipInfo"],
};
</script>
