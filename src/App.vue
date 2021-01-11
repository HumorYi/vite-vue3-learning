<template>
  <img alt="Vue logo" src="./assets/logo.png" />

  <select v-model="activeComponentName">
    <option v-for="item in components" :key="item.name" :value="item.name">
      {{ item.name }}
    </option>
  </select>

  <keep-alive>
    <component :is="activeComponentName" v-bind="activeComponentProps" v-on="activeComponentEvent"></component>
  </keep-alive>
</template>

<script lang="ts">
import { defineComponent, Ref, ref } from 'vue'
import Lifecycle from './components/Lifecycle.vue'
import Computed from './components/Computed.vue'
import Watch from './components/Watch.vue'

interface component {
  name: string
  props?: { [key]: any }
  event?: { [key]: Function }
}

export default defineComponent({
  name: 'App',
  components: {
    Lifecycle,
    Computed,
    Watch
  },
  setup() {
    const components = ref<component[]>([
      {
        name: 'Lifecycle',
        props: {
          msg: 'Hello Vue 3 + Vite'
        }
      },
      {
        name: 'Computed'
      },
      {
        name: 'Watch',
        event: {
          answer(question: string, answer: string) {
            console.log(`listen question : ${question}, answer : ${answer}`)
          }
        }
      }
    ])
    const activeComponentName = ref(components.value[components.value.length - 1].name)

    return {
      components,
      activeComponentName
    }
  },
  computed: {
    activeComponent(): component {
      return this.components.find((item: component) => item.name === this.activeComponentName)
    },
    activeComponentProps(): {} {
      return this.activeComponent.props || {}
    },
    activeComponentEvent(): {} {
      return this.activeComponent.event || {}
    }
  }
})
</script>

<style src="./app.sass" lang="sass"></style>
