<template>
  <div id="userLayout">
    <a-layout style="min-height: 100vh">
      <a-layout-header class="header">
        <a-space>
          <div class="logo">
            <icon-code :style="{ fontSize: '52px', color: '#000000' }" />
          </div>
          <div class="title">QI OJ</div>
        </a-space>
        <div
          style="color: rgba(0, 0, 0, 0.65); font-size: 14px; margin-top: 8px"
        >
          一个编程题目评测系统
        </div>
      </a-layout-header>
      <a-layout-content class="content">
        <router-view />
      </a-layout-content>
      <a-layout-footer class="footer">qioj by Qitx</a-layout-footer>
    </a-layout>
  </div>
</template>

<style scoped>
#userLayout {
  text-align: center;
  background: url("https://mdn.alipayobjects.com/yuyan_qk0oxh/afts/img/V-_oS6r-i7wAAAAAAAAAAAAAFl94AQBr")
    0% 0% / 100% 100%;
}

#userLayout .header {
  margin-top: 64px;
  margin-bottom: 16px;
}

#userLayout .content {
  margin-bottom: 16px;
  padding: 20px;
}

#userLayout .footer {
  padding: 16px;
  position: sticky;
  bottom: 0;
  left: 0;
  right: 0;
  text-align: center;
}

.logo {
  display: flex;
  align-items: center;
  height: 64px;
}

.title {
  color: black;
  font-size: 40px;
  font-weight: bold;
}
</style>
<script></script>
