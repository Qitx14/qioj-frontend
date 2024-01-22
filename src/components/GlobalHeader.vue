<template>
  <a-row id="globalHeader" align="center" :wrap="false">
    <a-col flex="auto">
      <a-menu
        mode="horizontal"
        :selected-keys="selectedKeys"
        @menu-item-click="doMenuClick"
      >
        <a-menu-item
          key="0"
          :style="{ padding: 0, marginRight: '38px' }"
          disabled
        >
          <div class="title-bar">
            <div class="logo">
              <icon-code :style="{ fontSize: '32px', color: '#000000' }" />
            </div>
            <div class="title">QI OJ</div>
          </div>
        </a-menu-item>
        <a-menu-item v-for="item in visibleRoutes" :key="item.path">
          {{ item.name }}
        </a-menu-item>
      </a-menu>
    </a-col>
    <a-col flex="100px">
      <div>
        {{ store.state.user?.loginUser?.userName ?? "未登录" }}
      </div>
    </a-col>
  </a-row>
</template>

<script setup lang="ts">
import { routes } from "@/router/routes";
import { useRouter } from "vue-router";
import { computed, ref } from "vue";
import { useStore } from "vuex";
import checkAccess from "@/access/checkAccess";
import ACCESS_ENUM from "@/access/accessEnum";

const router = useRouter();

const selectedKeys = ref(["/"]);

const store = useStore();

// const loginUser = ;

const visibleRoutes = computed(() => {
  return routes.filter((item, index) => {
    if (item.meta?.hideInMenu) {
      return false;
    }
    // 根据权限过滤菜单
    return checkAccess(
      store.state.user?.loginUser,
      item?.meta?.access as string
    );
  });
});

setTimeout(() => {
  store.dispatch("user/getLoginUser", {
    userName: "qitxAdmin",
    userRole: ACCESS_ENUM.ADMIN,
  });
}, 3000);

// 路由跳转后，更新对应选中的菜单项
router.afterEach((to, from, failure) => {
  selectedKeys.value = [to.path];
});
const doMenuClick = (key: string) => {
  router.push({
    path: key,
  });
};
</script>

<style scoped>
#globalHeader {
}

.title-bar {
  display: flex;
  align-items: center;
}

.logo {
  display: flex;
}

.title {
  color: black;
  font-size: large;
  font-weight: bold;
}
</style>
