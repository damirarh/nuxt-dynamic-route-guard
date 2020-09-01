<template>
  <div>
    <div>Path: {{ path }}</div>
    <nuxt-link to="1">1</nuxt-link>
    <nuxt-link to="2">2</nuxt-link>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { Route, NavigationGuardNext } from 'vue-router'

export default Vue.extend({
  beforeRouteEnter(to: Route, _from: Route, next: NavigationGuardNext) {
    console.log('beforeRouteEnter')
    next((vue: any) => {
      console.log(`beforeRouteEnter callback, uid = ${vue._uid}`)
      vue.path = to.path
    })
  },
  beforeRouteUpdate(to: Route, _from: Route, next: NavigationGuardNext) {
    console.log(`beforeRouteUpdate, uid = ${(this as any)._uid}`)
    this.path = to.path
    next()
  },
  beforeRouteLeave(_to: Route, _from: Route, next: NavigationGuardNext) {
    console.log(`beforeRouteLeave, uid = ${(this as any)._uid}`)
    next()
  },
  data() {
    return {
      path: '(default)',
    }
  },
  mounted() {
    console.log(`mounted, uid = ${(this as any)._uid}`)
  },
})
</script>
