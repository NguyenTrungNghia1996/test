<template>
  <a-layout>
    <a-layout-header class="header">
      <a-button v-if="isMobile" @click="toggleSider" class="menu-button">☰</a-button>
    </a-layout-header>
    
    <a-layout>
      <a-layout-content>
        <slot />
      </a-layout-content>
      
      <a-layout-sider v-if="isMobile" v-show="!collapsed" width="250" class="sider" placement="right">
        <a-menu mode="inline" theme="light" :selectedKeys="[selectedKey]">
          <a-menu-item key="1">Giới thiệu</a-menu-item>
          <a-sub-menu key="2">
            <template #title>Khóa học</template>
            <a-menu-item key="2-1">Khóa học A</a-menu-item>
            <a-menu-item key="2-2">Khóa học B</a-menu-item>
          </a-sub-menu>
          <a-menu-item key="3">Cuộc thi</a-menu-item>
          <a-menu-item key="4">Văn bản</a-menu-item>
          <a-menu-item key="5">Bài viết</a-menu-item>
        </a-menu>
      </a-layout-sider>
    </a-layout>
  </a-layout>
</template>

<script setup>
definePageMeta({ layout: "free" });
import { ref, onMounted } from 'vue';

const isMobile = ref(false);
const collapsed = ref(true);
const selectedKey = ref("1");

const checkScreenSize = () => {
  isMobile.value = window.innerWidth < 768;
  collapsed.value = true;
};

const toggleSider = () => {
  collapsed.value = !collapsed.value;
};

onMounted(() => {
  checkScreenSize();
  window.addEventListener('resize', checkScreenSize);
});
</script>

<!-- <style scoped>
.sider {
  height: 100vh;
  background: #fff;
  box-shadow: -2px 0 8px rgba(0, 0, 0, 0.1);
  transition: width 0.3s, opacity 0.3s;
  right: 0;
}
.header {
  display: flex;
  align-items: center;
  padding: 0 20px;
  background: #fff;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}
.menu-button {
  font-size: 20px;
  background: none;
  border: none;
  cursor: pointer;
  margin-left: auto;
}
</style> -->