<template>
    <div id="globalHeader">
      <!-- 自适应且不换行 -->
      <a-row :wrap="false">
        <!-- 栅格布局 -->
        <a-col flex="200px">
          <div class="title-bar">
            <img class="logo" src="../assets/logo.png" alt="logo" />
            <div class="title">鱼皮用户中心</div>
          </div>
        </a-col>
        <a-col flex="auto">
          <a-menu
            v-model:selectedKeys="current"
            mode="horizontal"
            :items="items"
            @click="doMenuClick"
          />
        </a-col>
        <a-col flex="80px">
          <div class="user-login-status">
            <div v-if="loginUserStore.loginUser.id">
              {{ loginUserStore.loginUser.username ?? "无名" }}
            </div>
            <div v-else>
              <a-button type="primary" href="/user/login">登录</a-button>
            </div>
          </div>
        </a-col>
      </a-row>
    </div>
</template>
<script lang="ts" setup>
import { h, ref } from 'vue';
import { MailOutlined, AppstoreOutlined, SettingOutlined } from '@ant-design/icons-vue';
import { MenuProps } from 'ant-design-vue';
import { CrownOutlined, HomeOutlined } from "@ant-design/icons-vue";
import { useRouter } from 'vue-router';
import { useLoginUserStore } from '@/store/useLoginUserStore';
// 引入一个钩子函数,创建路由跳转器
const router = useRouter()
// 点击菜单后的路由事件

// 定义一下，才能获取信息
const loginUserStore = useLoginUserStore()

// 接收key，指定key的数据类型（ts语法）
const doMenuClick = ({ key}:{key:string})=>{
  router.push({
    // 你点击菜单时，匹配路由规则上的路径，将其传入，然后跳转
      path:key
  })
}

const current = ref<string[]>(['mail']);

router.afterEach((to, from,failure) => {
  current.value = [to.path]
  // 响应式变量要访问其value
})

const items = ref<MenuProps["items"]>([
  {
    key: "/",
    icon: () => h(HomeOutlined),
    label: "主页",
    title: "主页",
  },
  {
    key: "/user/login",
    label: "用户登录",
    title: "用户登录",
  },
  {
    key: "/user/register",
    label: "用户注册",
    title: "用户注册",
  },
  {
    key: "/admin/userManage",
    icon: () => h(CrownOutlined),
    label: "用户管理",
    title: "用户管理",
  },
  {
    key: "others",
    label: h(
      "a",
      { href: "https://www.codefather.cn", target: "_blank" },
      "编程导航"
    ),
    title: "编程导航",
  },
]);
</script>

<style scoped>
  .title-bar {
  display: flex;
  align-items: center;
}

.title {
  color: black;
  font-size: 18px;
  margin-left: 16px;
}

.logo {
  height: 48px;
}
</style>