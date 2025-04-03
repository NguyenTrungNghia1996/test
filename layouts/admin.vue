<template>
  <div class="w-full h-screen flex flex-col bg-gray-200">
    <div class="h-15">
      <BaseAdminHeader />
    </div>
    <div class="w-full flex-1 flex overflow-hidden">
      <BaseAdminMenu />
      <div class="flex-1 overflow-y-auto">
        <div class="bg-white sticky top-0 !z-10">
          <BaseAdminBreadcrumb />
        </div>
        <div class="p-2 w-full">
          <slot />
        </div>
      </div>
    </div>
  </div>
</template>
