<script setup lang="ts">
interface AppState {
  name: string;
  rawHtml: string;
}

const state = reactive<AppState>({
  name: "PHNam (TrippleN)",
  rawHtml: "<span style='color: red'>Xiao</span>",
});

const anotherState = shallowReactive({
  foo: 1,
  nested: {
    bar: 2,
  },
});

const count = ref<number>(0);

const increaseCount = () => {
  count.value++;
};

const doubleCount = computed<number>(() => count.value * 2);

watch([count, doubleCount], ([newCount, newDoubleCount]): void => {
  console.log(`Count: ${newCount}, doubleCount: ${newDoubleCount}`);
});

anotherState.nested.bar++;
</script>

<template>
  <div>
    <p>Hello {{ state.name }}!</p>
    <p v-html="state.rawHtml"></p>
    <!-- Ref auto unwrapping in template, no need to use .value -->
    <p>Count: {{ count }}</p>
    <p>Double count: {{ doubleCount }}</p>
    <button @click="increaseCount">Increase</button>
    <p>{{ anotherState.nested.bar }}</p>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
