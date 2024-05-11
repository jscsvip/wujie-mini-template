<template>
  <div class="title">子应用2: MICRO-TWO</div>
  <div style="font-weight: bold; line-height: 38px">
    {{ "micro2.count:" + count }}
  </div>
  <div><button @click="change1">修改 micro1.number 的值为 20</button></div>
  <div><button @click="changeMain">修改 main.tag 的值为 55</button></div>
</template>
<script setup>
import { ref, onMounted, onUnmounted } from "vue";
const count = ref(2);
const change1 = () => {
  window.$wujie.bus.$emit("change1", 20);
};
const changeMain = () => {
  window.$wujie.bus.$emit("changeMain", 55);
};
onMounted(() => {
  window.$wujie.bus.$on("change2", (val) => {
    count.value = val;
  });
});
onUnmounted(() => {
  window.$wujie.bus.$off("change2");
});
</script>
<style scoped>
.title {
  color: blueviolet;
  font-weight: bolder;
}
</style>
