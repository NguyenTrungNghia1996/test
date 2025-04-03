<template>
  <div>
    <h1>Dashboard</h1>
    <p>Welcome to the dashboard!</p>
  </div>
</template>
<script setup>
definePageMeta({ layout: "admin" });
const nuxtApp = useNuxtApp();
const t = nuxtApp.$i18n.t;
onMounted(() => {
  ////////////////////////////////Breadcrumb
  const settingStore = useSettingStore();
  const tempBreadcrumb = computed(() => {
    return [
      { url: "/admin/dashboard", title: t("dashboard") },
      { url: "/admin/dashboard", title: t("dashboard") },
    ];
  });
  settingStore.setBreadcrumb(tempBreadcrumb.value);
  watch(tempBreadcrumb, () => {
    settingStore.setBreadcrumb(tempBreadcrumb.value);
  });
});
</script>