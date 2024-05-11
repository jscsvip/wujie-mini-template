<template>
  <div class="title">子应用: MICRO-ONE</div>
  <div style="font-weight: bold; line-height: 38px">
    {{ "micro1.number:" + number }}
  </div>
  <div><button @click="change2">修改 micro2.count 的值为 10</button></div>
  <div><button @click="changeMain">修改 main.tag 的值为 44</button></div>
  <div>{{ "主应用传过来的值:" + data }}</div>
  <div><button @click="exctMain">执行主应用的方法</button></div>
</template>
<script setup>
import { ref, onMounted, onUnmounted } from "vue";
const number = ref(1);
const data = window.$wujie.props.data;

const change2 = () => {
  window.$wujie.bus.$emit("change2", 10);
};
const changeMain = () => {
  window.$wujie.bus.$emit("changeMain", 44);
};
const exctMain = () => {
  window.$wujie.props.method.propsMethod();
};
onMounted(() => {
  window.$wujie.bus.$on("change1", (val) => {
    number.value = val;
  });
});
onUnmounted(() => {
  window.$wujie.bus.$off("change1");
});
</script>
<style scoped>
.title {
  color: blueviolet;
  font-weight: bolder;
}
</style>
