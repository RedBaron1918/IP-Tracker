<template>
  <div
    class="absolute -bottom-5 lg:-bottom-20 flex flex-row bg-white gap-y-2 gap-x-12 px-8 pt-8 pb-4 rounded-md lg:mb-14"
  >
    <div class="flex flex-col">
      <h3 class="text-xs mb-2 uppercase">Ip Address</h3>
      <span class="text-2xl">{{ IPinfo.address }}</span>
    </div>

    <div class="flex flex-col">
      <h3 class="text-xs mb-2 uppercase">Location</h3>
      <span class="text-2xl">{{ IPinfo.state }}</span>
    </div>

    <div class="flex flex-col">
      <h3 class="text-xs mb-2 uppercase">TimeZone</h3>
      <span class="text-2xl">{{ IPinfo.timezone }}</span>
    </div>

    <div class="flex flex-col">
      <h3 class="text-xs mb-2 uppercase">Isp</h3>
      <span class="text-2xl">{{ IPinfo.isp }}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: ["IPinfo"],
};
</script>
