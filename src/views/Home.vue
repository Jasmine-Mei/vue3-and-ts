<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" />
    <div>{{ data.mag }} || {{ msg }}</div>
    <div>1.----{{ num1 }}</div>
    <div>2.-----{{ data.num2 }}</div>
    <div>sum:{{ sum }}</div>
    <button @click="handleNumberAdd">按钮</button>
  </div>
</template>

<script lang="ts">
import {
  computed,
  ComputedRef,
  defineComponent,
  nextTick,
  onMounted,
  onUnmounted,
  onUpdated,
  reactive,
  Ref,
  ref,
  watch,
} from 'vue';
import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src

interface DataProps {
  num2: number;
}

export default defineComponent({
  name: 'Home',
  components: {
    HelloWorld,
  },
  setup() {
    // const data = reactive({
    //   mag: 'I`m OK',
    // }); // reactive 定义值

    const msg = ref('你好'); // ref 定义值

    // reactive ref 更改值

    // ref 适合基础数据类型的响应
    // ref 代理的对象值会只想 property .value
    const num1: Ref<number> = ref(1);

    // reactive 适合引用数据类型的相应
    const data: DataProps = reactive({
      num2: 2,
    });

    const sum: ComputedRef<number> = computed(() => {
      return num1.value + data.num2;
    });

    function handleNumberAdd(): void {
      num1.value++;
      data.num2++;
      num.value++;
    }
    const num: Ref<number> = ref(1);
    watch(num, (newVal, oldVal) => {
      console.log(newVal, oldVal);
    });

    // 各个生命周期变化
    onMounted(() => {
      console.log('mounted');
    });
    nextTick(() => {
      console.log('nextTick');
    });
    onUpdated(() => {
      console.log('updated');
    });
    onUnmounted(() => {
      console.log('Unmounted');
    });

    return {
      data,
      msg,
      num1,
      sum,
      handleNumberAdd,
    };
  },
});
</script>
