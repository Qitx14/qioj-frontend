<template>
  <div id="app">
    <BasicLayout />
  </div>
</template>

<style>
#app {
}
</style>
<script setup lang="ts">
import BasicLayout from "@/layouts/BasicLayout";
import { useRouter } from "vue-router";
import { useStore } from "vuex";
import ACCESS_ENUM from "@/access/accessEnum";
import { onMounted } from "vue";

const router = useRouter();
const store = useStore();

/**
 * 全局初始化函数，有全局单次调用的代码，都可以写道这里
 */
const doInit = () => {
  console.log("hello");
};

onMounted(() => {
  doInit();
});

router.beforeEach((to, from, next) => {
  // 仅管理员可见，判断当前用户是否有权限
  // 当前页面需要管理员权限
  if (to.meta?.access === ACCESS_ENUM.ADMIN) {
    // 但是当前登录用户没有管理员权限
    if (store.state.user?.loginUser?.role !== "admin") {
      next("/noAuth");
      return;
    }
  }
  next();
});
</script>
