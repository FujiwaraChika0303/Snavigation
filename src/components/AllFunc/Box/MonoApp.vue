<template>
  <div class="memo-app">
    <n-space vertical>
      <n-input
        v-model:value="newMemo"
        placeholder="请输入备忘内容..."
        clearable
        @keypress.enter="addMemo"
      />
      <n-button type="info" @click="addMemo">添加备忘</n-button>
      <n-list>
        <n-list-item
          v-for="(memo, index) in memos"
          :key="index"
          class="memo-item"
        >
          <div class="memo-content">{{ memo }}</div>
          <n-button
            type="error"
            size="small"
            @click="deleteMemo(index)"
          >删除</n-button>
        </n-list-item>
      </n-list>
    </n-space>
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue';
import {
  NInput,
  NButton,
  NList,
  NListItem,
  NSpace
} from 'naive-ui';

const newMemo = ref('');
const memos = ref([]);

// 当组件挂载时，从localStorage加载备忘录数据
onMounted(() => {
  const savedMemos = localStorage.getItem('memos');
  if (savedMemos) {
    memos.value = JSON.parse(savedMemos);
  }
});

// 观察memos数组的变化，并将其保存到localStorage
watch(memos, (newMemos) => {
  localStorage.setItem('memos', JSON.stringify(newMemos));
}, { deep: true });

const addMemo = () => {
  if (!newMemo.value.trim()) return;
  memos.value.push(newMemo.value.trim());
  newMemo.value = '';
};

const deleteMemo = (index) => {
  memos.value.splice(index, 1);
};
</script>

<style scoped>
.memo-app {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

.memo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.memo-content {
  margin-right: 20px;
}
</style>
