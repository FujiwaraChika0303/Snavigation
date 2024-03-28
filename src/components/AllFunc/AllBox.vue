<template>
  <n-tabs class="all-box" size="large" justify-content="space-evenly" animated>
    <n-tab-pane class="no-padding" name="link" tab="捷径">
      <ShortCut />
    </n-tab-pane>
    <n-tab-pane name="Music" tab="音乐"> 还没写 </n-tab-pane>
    <n-tab-pane name="more" tab="待办"> 过段时间吧 </n-tab-pane>
  </n-tabs>
</template>

<script setup>
import { NTabs, NTabPane } from "naive-ui";
import ShortCut from "@/components/AllFunc/Box/ShortCut.vue";
</script>
