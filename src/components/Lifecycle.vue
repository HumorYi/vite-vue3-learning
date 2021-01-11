<template>
  <h1>LifeCycle: {{ msg }}</h1>
  <p>count is: {{ count }}</p>
  <section>
    <button @click="increment">increment</button>
    <button @click="decrement">decrement</button>
  </section>
</template>

<script lang="ts">
import { ref, defineComponent } from 'vue'

export default defineComponent({
  name: 'Lifecycle',
  props: {
    msg: {
      type: String,
      required: true,
      validator: value => value !== ''
    }
  },
  setup: () => {
    const count = ref(0)

    const increment = () => count.value++
    const decrement = () => count.value--

    return { count, increment, decrement }
  },
  beforeCreate() {
    console.log('beforeCreate')
  },
  created() {
    console.log('created')
  },
  beforeMount() {
    console.log('beforeMount')
  },
  mounted() {
    console.log('mounted')
  },
  beforeUpdate() {
    console.log('beforeUpdate')
  },
  updated() {
    console.log('updated')
  },
  beforeUnmount() {
    console.log('beforeUnmount')
  },
  unmounted() {
    console.log('unmounted')
  }
})
</script>

<style scoped>
a {
  color: #42b983;
}
</style>
