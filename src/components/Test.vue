
<template>
  <div>
    <div>props:{{ props.data.title }}</div>
    <button @click="emitEvent">emit</button>
    <div>{{ info.info }}</div>
  </div>
</template>


<script setup>
import {
  toRef,
  toRefs,
  defineEmits,
  defineProps,
  inject,
  watch,
  watchEffect,
} from "vue";

const props = defineProps({
  data: Object,
});
const info = inject("info");
const { data } = toRefs(props);
const refData = toRef(props, "data");
// console.log(data.value === props.data, refData.value === props.data);

const emit = defineEmits(["eventUpdate"]);

const emitEvent = () => {
  emit("eventUpdate", 123);
};
watch(props, (newValue, oldValue) => {
  console.log(newValue.data.title, oldValue.data.title);
});
// watchEffect(() => {});
</script>

<style scoped>
</style>
