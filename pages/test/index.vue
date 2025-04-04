<template>
  <div>
    <a-menu mode="horizontal" theme="light" :selectedKeys="[selectedKey]">
      <span>
        <a-menu-item v-for="m in menu" :key="m.key" @click="handleClick(m.key)">
          {{ m.title }}
        </a-menu-item>
      </span>

      <!-- <a-menu-item key="1">Giới thiệu</a-menu-item>
      <a-sub-menu key="2">
        <template #title>Khóa học</template>
<a-menu-item key="2-1">Khóa học A</a-menu-item>
<a-sub-menu key="2-2">
  <template #title> Khóa học B</template>
  <a-menu-item key="2-2-1-1" @click="handleClick('2-2-1-1')">Khóa học B1.1</a-menu-item>
  <a-menu-item key="2-2-1-2">Khóa học B1.2</a-menu-item>
</a-sub-menu>
</a-sub-menu>
<a-menu-item key="3">Cuộc thi</a-menu-item>
<a-menu-item key="4">Văn bản</a-menu-item>
<a-menu-item key="5">Bài viết</a-menu-item> -->
    </a-menu>

    {{ selectedKey }}
  </div>
</template>

<script setup>
definePageMeta({ layout: "free" });
const selectedKey = ref("");
const handleClick = (e) => {
  selectedKey.value = e;
}
const menu = ref([
  {
    key: "1",
    title: "Giới thiệu",
    url: "/test/intro",
  },
  {
    key: "2",
    title: "Khóa học",
    url: "/test/course",
    child: [
      {
        key: "2-1",
        title: "Khóa học A",
        url: "/test/course/course-a",
      },
      {
        key: "2-2",
        title: "Khóa học B",
        url: "/test/course/course-b",
        child: [
          {
            key: "2-2-1-1",
            title: "Khóa học B1.1",
            url: "/test/course/course-b/course-b1-1",
          },
          {
            key: "2-2-1-2",
            title: "Khóa học B1.2",
            url: "/test/course/course-b/course-b1-2",
          },
        ],
      },
    ],
  },
  {
    key: "3",
    title: "Cuộc thi",
    url: "/test/contest",
  },
  {
    key: "4",
    title: "Văn bản",
    url: "/test/document",
  },
  {
    key: "5",
    title: "Bài viết",
    url: "/test/article",
  },
]);
</script>
