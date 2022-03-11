<template>
  <div>
    <div>ref:{{ refValue }}</div>
    <button @click="setRef">refValue value 123</button>
    <div>reactive:{{ book.title }}</div>
    <button @click="setReactive">reactive value 123</button>

    <div ref="dom"></div>
  </div>
  <Test :data="testData" @eventUpdate="eventUpdate"></Test>
</template>


<script setup>
// beforeCreate	setup
// created	setup
// beforeMount	onBeforeMount
// mounted	onMounted
// beforeUpdate	onBeforeUpdate
// updated	onUpdated
// beforeDestory	onBeforeUnmount
// destoryed	onUnmounted
// script-setup 无法指定当前组件的名字，所以使用的时候以文件名为主
// reactive 用于为对象添加响应式状态
// ref 用于为数据添加响应式状态
// toRef 用于为源响应式对象上的属性新建一个ref，从而保持对其源对象属性的响应式连接
// toRefs 用于将响应式对象转换为结果对象，其中结果对象的每个属性都是指向原始对象相应属性的ref
import { ref, reactive, provide, getCurrentInstance } from "vue";
import {
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  // unMounted,
} from "vue";
import Test from "../../components/Test.vue";
// provide && inject
provide("info", { info: "info" });
const refValue = ref("refValue");
const setRef = () => {
  refValue.value = 123;
};

const book = reactive({ title: "Vue 3 Guide" });
const setReactive = () => {
  book.title = 123;
};

const testData = reactive({ title: "title" });

const eventUpdate = (value) => {
  testData.title = value;
};

const dom = ref("dom");

onBeforeMount(() => {
  // 在挂载前执行某些代码
});

onMounted(() => {
  // 在挂载后执行某些代码
  dom.value.innerHTML = 123;
  console.log(getCurrentInstance());
});

onBeforeUpdate(() => {
  // 在更新前前执行某些代码
});

onUpdated(() => {
  // 在更新后执行某些代码
});

onBeforeUnmount(() => {
  // 在组件销毁前执行某些代码
});

// unMounted(() => {
//   // 在组件销毁后执行某些代码
// });
</script>

<style scoped>
</style>