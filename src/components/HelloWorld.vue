<template>
  <h3>{{ msg }}</h3>
  <p>
    counter :{{counter}}
  </p>
  <p>
    <a href="https://vitejs.dev/guide/features.html" target="_blank"
      >Vite Documentation</a
    >
    |
    <a href="https://v3.vuejs.org/" target="_blank">Vue 3 Documentation</a>
  </p>

  <button
    @click="
      state.counter++;
      state.tripleCounter();      
    "
  >
    state.count is: {{ state.counter }}
  </button>
  <p style="color: #42b983">copyState.count is : {{ copyState.counter }} </p>
  <p>state.double:{{ state.doubleCounter }}</p>
  

  <p>
    Edit
    <code>components/HelloWorld.vue</code> to test hot module replacement.
  </p>
</template>

<script setup>
import { defineProps, ref, reactive, computed,readonly,watchEffect } from "vue";

defineProps({
  msg: String,
});

const counter = ref(0);
// Ref Unwrapping : 1.reactive object 2.tempate 
const state = reactive({
  counter,
  doubleCounter: computed(() => state.counter * 2),
  tripleCounter() {
    this.counter = this.counter * 3;
  },
});

setTimeout(() => {
  counter.value++
  // -> logs 1
}, 100)
// setInterval(
//   () => {
//   counter.value++  
// }, 1000
// )

watchEffect(() => console.log("the counter value : "+counter.value))
// copyState using readonly(obj) , so it's own property value can be changed ,👍it will cause warning , not error
const copyState = readonly(state)
// const doubleCounter=computed(()=>state.counter *2)
// dynamic property

let websiteName = "pjchender";
let a = 2;
let b = 3;

let obj_es = {
  [websiteName]: "welcome",
  [a+b]: "sumNumber"
}
console.log(obj_es);  // [Object]{5: "sumNumber", pjchender: "welcome"}



</script>

<style scoped>
a {
  color: #42b983;
}
</style>