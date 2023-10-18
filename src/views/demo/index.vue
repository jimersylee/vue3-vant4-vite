<script setup lang="ts">
import {reactive, ref} from "vue";
import {showToast} from "vant";

const list = ref([]);
const loading = ref(false);
const finished = ref(false);
const value = ref('');
const onSearch = (val) => showToast(val);
const onCancel = () => showToast('取消');
const onLoad = () => {
  loading.value = true;
  setTimeout(() => {
    for (let i = 0; i < 10; i++) {
      list.value.push("item");
    }
    loading.value = false;
    if (list.value.length >= 6) {
      finished.value = true;
    }
  }, 500);
};
</script>

<template>
  <div class="demo-content px-[12px]">
    <form action="/">
      <van-search
          v-model="value"
          show-action
          placeholder="请输入搜索关键词"
          @search="onSearch"
          @cancel="onCancel"
      />
    </form>
    <van-divider class="my-[12px]" />
    <van-tabs>
      <van-tab title="客厅">
        <van-list
            v-model:loading="loading"
            :finished="finished"
            finished-text="没有更多了"
            @load="onLoad"
        >
          <van-cell v-for="item in list" :key="item" :title="item" />
        </van-list>
      </van-tab>
      <van-tab title="卧室1">
        <van-empty image="search" description="没有更多了" />
      </van-tab>
      <van-tab title="卧室2">没有</van-tab>
      <van-tab title="卫生间">没有</van-tab>
    </van-tabs>

  </div>
</template>
