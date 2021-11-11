<template>
  <div id="app">
    <img alt="Vue logo" src="https://vuejs.org/images/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <button @click="subtractCount">-</button>
    <p>Count: {{ count }}</p>
    <button @click="addCount">+</button>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import { reactive, toRefs, watch } from 'vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
  },
  setup(props, context) {
    const state = reactive({
      count: 0,
    });
    const subtractCount = () => {
      state.count -= 1;
    };
    const addCount = () => {
      state.count += 1;
    };
    watch(
      () => state.count,
      (currentCount, prevCount) => {
        console.log('currentCount:', currentCount);
        console.log('prevCount:', prevCount);
      }
    );
    return {
      ...toRefs(state),
      subtractCount,
      addCount,
    };
  },
};
</script>

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
