<template>
  <h1>Home</h1>
  <button @click="throwError">Throw error</button>
  <p>
    <img src="../assets/logo.png" alt="logo" />
  </p>
  <button @click="state.count++">count is: {{ state.count }}</button>
  <Foo />
  <p class="virtual">msg from virtual module: {{ foo.msg }}</p>
  <p class="inter">this will be styled with a font-face</p>

  <ImportType />
</template>

<script setup>
import foo from '@foo'
import { reactive, defineAsyncComponent } from 'vue'
const ImportType = load('ImportType')
const Foo = defineAsyncComponent(() =>
  import('../components/Foo').then((mod) => mod.Foo)
)
function load(file) {
  return defineAsyncComponent(() => import(`../components/${file}.vue`))
}
function throwError() {
      throw new Error('Sentry Error')
}
const state = reactive({ count: 0 })
</script>

<style scoped>
h1,
a {
  color: green;
}
</style>
