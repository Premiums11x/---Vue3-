<template>
  <div id="app">
    <BasicLayout/>
  </div>

</template>

<style>

</style>

<script setup lang="ts">
import BasicLayout from "../layouts/BasicLayout.vue"
import { useLoginUserStore } from "@/store/useLoginUserStore";
// 全局获取登录信息
const loginUserStore = useLoginUserStore();
loginUserStore.fetchLoginUser();
</script>