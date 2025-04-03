<template>
  <div class="container mx-auto h-full flex justify-between items-center">
    <img src="https://study.vnpost.vn/static/images/trangchu.png" alt="Vietnam Post" class="h-10 m-4">
    <div class="flex items-center">
      <a-menu class="border-b-0" v-if="smAndLarger" :open-keys="state.openKeys" v-model:selectedKeys="selectedKeys" mode="horizontal" :key="locale" @openChange="onOpenChange">
        <template v-for="item_menu in renderMenu()" :key="item_menu.key">
          <a-sub-menu v-if="item_menu.child && item_menu.child.length > 0" :key="item_menu.key">
            <template #title>
              {{ item_menu.title }}
            </template>
            <a-menu-item v-for="child_menu_item in item_menu.child" :key="child_menu_item.key">
              <div @click="router_push(child_menu_item.url)">
                {{ child_menu_item.title }}
              </div>
            </a-menu-item>
          </a-sub-menu>
          <a-menu-item v-else :key="item_menu.url" @click="router_push(item_menu.url)">
            {{ item_menu.title }}
          </a-menu-item>
        </template>
      </a-menu>
    </div>
    <div class="flex space-x-3 items-center">
      <a-badge count="2" dot="true">
        <Icon name="ant-design:bell-outlined" class="text-xl flex justify-center" />
      </a-badge>
      <Icon name="ant-design:question-circle-outlined" class="text-xl flex justify-center" />
      <a-avatar>
        <template #icon>
          <UserOutlined />
        </template>
      </a-avatar>
      <div v-if="!smAndLarger">
        <Icon @click="drawerVisible = true" name="ant-design:menu-outlined" class="flex text-xl justify-center mr-3" />
        <a-drawer v-model:visible="drawerVisible" placement="right" title="Menu" :closable="true">
          <a-menu class="!border-0" :open-keys="state.openKeys" v-model:selectedKeys="selectedKeys" mode="inline" :key="locale" @openChange="onOpenChange">
            <template v-for="item_menu in renderMenu()" :key="item_menu.key">
              <a-sub-menu v-if="item_menu.child && item_menu.child.length > 0" :key="item_menu.key">
                <template #title>
                  {{ item_menu.title }}
                </template>
                <a-menu-item v-for="child_menu_item in item_menu.child" :key="child_menu_item.key">
                  <div @click="router_push(child_menu_item.url)">
                    {{ child_menu_item.title }}
                  </div>
                </a-menu-item>
              </a-sub-menu>
              <a-menu-item v-else :key="item_menu.url" @click="router_push(item_menu.url)">
                {{ item_menu.title }}
              </a-menu-item>
            </template>
          </a-menu>
        </a-drawer>
      </div>

    </div>
  </div>
</template>
<script setup>
const nuxtApp = useNuxtApp();
const t = nuxtApp.$i18n.t;
import { breakpointsTailwind, useBreakpoints } from "@vueuse/core";
const { locale, locales, setLocale } = useI18n();
const breakpoints = useBreakpoints(breakpointsTailwind);
const smAndLarger = breakpoints.greaterOrEqual("sm");
const mdAndLarger = breakpoints.greaterOrEqual("md");
const lgAndLarger = breakpoints.greaterOrEqual("lg");

const router = useRouter();
const selectedKeys = ref([]);
const collapsed = ref(false);
const isMobile = ref("hidden");
watch(mdAndLarger, () => {
  if (!mdAndLarger.value && !collapsed.value) {
    collapsed.value = true;
    isMobile.value = "hidden";
  }
});
watch(lgAndLarger, () => {
  if (lgAndLarger.value && collapsed.value) {
    collapsed.value = false;
    isMobile.value = "block";
  }
});

import { useUserStore } from "~~/stores/userStore";
const userStore = useUserStore();

const drawerVisible = ref(false);

const state = reactive({
  openKeys: [],
});
const onOpenChange = openKeys => {
  if (openKeys.length > 0) {
    state.openKeys = [openKeys.at(openKeys.length - 1)];
  } else {
    state.openKeys = openKeys;
  }
};
// const menuUser = computed(() => {
//   return [
//     {
//       id: nuxtApp.$RANDOMID(),
//       title: t("question-repository"),
//       icon: "ant-design:file-unknown-outlined",
//       url: "/question",
//       key: "questionManage",
//       child: [
//         { id: nuxtApp.$RANDOMID(), title: t("add-individual-question"), url: "/question", key: "/question" },
//         { id: nuxtApp.$RANDOMID(), title: t("add-questions-from-a-file"), url: "/question/file", key: "/question/file" },
//         { id: nuxtApp.$RANDOMID(), title: t("view-and-edit-questions"), url: "/question/view", key: "/question/view" },
//       ],
//     },
//     {
//       id: nuxtApp.$RANDOMID(),
//       title: t("exam-setup"),
//       icon: "ant-design:folder-open-outlined",
//       key: "examManage",
//       child: [
//         { id: nuxtApp.$RANDOMID(), title: t("generate-a-test-from-a-file"), url: "/exam/file", key: "/exam/file" },
//         { id: nuxtApp.$RANDOMID(), title: t("generate-a-test-from-the-database"), url: "/exam/database", key: "/exam/database" },
//         { id: nuxtApp.$RANDOMID(), title: t("manage-original-exams"), url: "/exam/original", key: "/exam/original" },
//       ],
//     },
//     {
//       id: nuxtApp.$RANDOMID(),
//       title: t("mark-the-test"),
//       icon: "ant-design:container-outlined",
//       key: "mark",
//       child: [
//         { id: nuxtApp.$RANDOMID(), title: t("mark-the-test"), url: "/mark", key: "/mark" },
//         { id: nuxtApp.$RANDOMID(), title: t("result-mark"), url: "/mark/result", key: "/mark/result" },
//       ],
//     },
//   ];
// });
// console.log(userStore.user.role, "userStore.user.role");
const menuAdmin = computed(() => {
  return [
    { id: nuxtApp.$RANDOMID(), title: "Giới Thiệu", url: "/admin/dashboard", icon: "ant-design:dashboard-outlined", key: "/admin/dashboard" },
    {
      id: nuxtApp.$RANDOMID(),
      title: "Khoá Học",
      icon: "ant-design:team-outlined",
      key: "unit-manage",
      child: [
        { id: nuxtApp.$RANDOMID(), title: "Danh sách khoá học", url: "/manage/user", key: "/manage/user" },
        { id: nuxtApp.$RANDOMID(), title: "Đăng ký khoá học", url: "/manage/userType", key: "/manage/userType" },
        { id: nuxtApp.$RANDOMID(), title: "Đề xuất nhu cầu", url: "/manage/group", key: "/manage/group" },
      ]
    },
    {
      id: nuxtApp.$RANDOMID(),
      title: "Cuộc thi",
      key: "examManage",
    },
    {
      id: nuxtApp.$RANDOMID(),
      title: "Văn bản",
      key: "document",
      child: [
        { id: nuxtApp.$RANDOMID(), title: "Danh sách văn bản", url: "/document/list", key: "/document/list" },
        { id: nuxtApp.$RANDOMID(), title: "Thêm văn bản", url: "/document/add", key: "/document/add" },
      ]
    }
  ];
});

function renderMenu() {
  // if (userStore.user.role == "user") {
  //   if (userStore.user.user_type == `admin`) return menuAdmin.value.filter(el => el.id !== `mark`);
  //   else return menuUser.value;
  // }
  // if (userStore.user.role == "admin") return menuAdmin.value;
  return menuAdmin.value
}
// function router_push(url) {
//   router.push(url);
// }
const router_push = async url => {
  await navigateTo(url);
};
watch(
  () => router.currentRoute.value.fullPath,
  (newValue, oldValue) => {
    selectedKeys.value = [router.currentRoute.value.fullPath];
  },
);
onMounted(() => {
  selectedKeys.value = [router.currentRoute.value.fullPath];
  if (userStore.user.role === "user") {
    if (userStore.user.user_type === "admin") {
      const item = menuAdmin.value.find(el => el.child && el.child.findIndex(el => el.url === router.currentRoute.value.fullPath) >= 0);
      if (item) state.openKeys = [item.key];
    } else {
      const item = menuUser.value.find(el => el.child && el.child.findIndex(el => el.url === router.currentRoute.value.fullPath) >= 0);
      if (item) state.openKeys = [item.key];
    }
  } else {
    const item = menuAdmin.value.find(el => el.child && el.child.findIndex(el => el.url === router.currentRoute.value.fullPath) >= 0);
    if (item) state.openKeys = [item.key];
  }
});
</script>