<template>
  <div>
    <TypeC></TypeC>
    <LazyTypeD></LazyTypeD>
    <TypeE></TypeE>

    <div>
      here↓ A or B
      <suspense>
        <component :is="componentType"/>
      </suspense>
      here↑ A or B
    </div>
    <button @click="toggleComponent">touch me!</button>

    <div>
      <div>
        here↓ F or G
        <component :is="componentTypeWithoutSuspense"></component>
        here↑ F or G
      </div>
      <button @click="toggleComponent2">touch me!</button>
    </div>

    <div>
      <div>
        here↓ H or J
        <component :is="normalComponentType"></component>
        here↑ H or J
      </div>
      <button @click="toggleComponent3">touch me!</button>
    </div>

    <div>
      <div>
        here↓ K or L
        <LazyTypeK v-if="flag"></LazyTypeK>
        <LazyTypeL v-else></LazyTypeL>
        here↑ K or L
      </div>
      <button @click="flag = !flag">touch me!</button>
    </div>
  </div>
</template>

<script setup>
const TypeE = defineAsyncComponent(() => import('/components/TypeE.vue'));

const TypeA = defineAsyncComponent(() => import('/components/TypeA.vue'));
const TypeB = defineAsyncComponent(() => import('/components/TypeB.vue'));
const componentTypeStr = ref('a');
const toggleComponent = () =>
  (componentTypeStr.value = componentTypeStr.value === 'a' ? 'b' : 'a');
const componentType = computed(() => {
  return componentTypeStr.value === 'a' ? TypeA : TypeB;
});

const TypeF = defineAsyncComponent(() => import('/components/TypeF.vue'));
const TypeG = defineAsyncComponent(() => import('/components/TypeG.vue'));
const componentTypeWithoutSuspenseStr = ref('f');
const toggleComponent2 = () =>
  (componentTypeWithoutSuspenseStr.value =
    componentTypeWithoutSuspenseStr.value === 'f' ? 'g' : 'f');
const componentTypeWithoutSuspense = computed(() => {
  return componentTypeWithoutSuspenseStr.value === 'f' ? TypeF : TypeG;
});

import TypeH from '@/components/TypeH.vue';
import TypeJ from '@/components/TypeJ.vue';
const normalComponentTypeStr = ref('h');
const toggleComponent3 = () =>
  (normalComponentTypeStr.value =
    normalComponentTypeStr.value === 'h' ? 'j' : 'h');
const normalComponentType = computed(() => {
  return normalComponentTypeStr.value === 'h' ? TypeH : TypeJ;
});

const flag = ref(true);
</script>
