<template>
  <div>
    <a-config-provider :theme="theme" :locale="locale">
      <a-extract-style>
        <NuxtLayout>
          <NuxtPage />
        </NuxtLayout>
      </a-extract-style>
    </a-config-provider>

  </div>
</template>
<script setup>
import vi_VN from "ant-design-vue/es/locale/vi_VN";
const locale = computed(() => {
  return vi_VN;
});
const theme = computed(() => {
  return {
    token: {
      colorPrimary: "#f69b02",
    },
  };
});
</script>
