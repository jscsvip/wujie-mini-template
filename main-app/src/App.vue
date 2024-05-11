<template>
  <div class="main-box">
    <div class="title">
      主应用
      <div>mian.tag: {{ tag }}</div>
      <div><button @click="change1">修改 micro1.number 的值为 666</button></div>
      <div><button @click="change2">修改 micro2.count 的值为 999</button></div>
    </div>
    <WujieVue
      class="item"
      name="micro1"
      url="http://127.0.0.1:3031"
      width="100%"
      height="100%"
      :sync="true"
      :props="{ data: '我是主应用的数据', method: { propsMethod } }"
    ></WujieVue>
    <WujieVue
      class="item"
      name="micro2"
      url="http://127.0.0.1:3032"
      width="100%"
      height="100%"
      :sync="true"
    ></WujieVue>
  </div>
  <div class="button-box"></div>
</template>
<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import wujie from "wujie-vue3";
const tag = ref(0);
const change1 = () => {
  wujie.bus.$emit("change1", 666);
};
const change2 = () => {
  wujie.bus.$emit("change2", 999);
};
const propsMethod = () => {
  alert("我是主应用的方法");
};
onMounted(() => {
  wujie.bus.$on("changeMain", (val) => {
    tag.value = val;
  });
});
onUnmounted(() => {
  wujie.bus.$off("changeMain");
});
</script>

<style lang="less" scoped>
.item {
  border: 1px dashed #ccc;
  border-radius: 8px;
  margin: 20px;
}
.title {
  .item;
  height: 100%;
  width: 100%;
  line-height: 38px;
  color: rgb(41, 22, 80);
  font-weight: bold;
  text-align: center;
}
.main-box {
  height: 250px;
  width: 100%;
  display: flex;
  align-items: center;
  flex-wrap: nowrap;
}
.button-box {
  height: 250px;
  width: 100%;
  display: flex;
  align-items: center;
  flex-wrap: nowrap;
}
</style>
