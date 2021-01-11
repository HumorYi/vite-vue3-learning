<template>
  <h1>Computed:</h1>
  <p>firstNamePrefix: {{ firstNamePrefix }}</p>
  <p>fullName: {{ fullName }}</p>
  <section>
    <button @click="setFullName">setFullName</button>
  </section>
</template>

<script lang="ts">
import { ref, defineComponent } from 'vue'

export default defineComponent({
  name: 'Computed',
  data() {
    return {
      firstName: '饿马',
      lastName: '摇铃'
    }
  },
  computed: {
    fullName: {
      get(): string {
        return this.firstName + ' ' + this.lastName
      },
      set(newValue: string) {
        const names = newValue.split(' ')
        this.firstName = names[0]
        this.lastName = names[names.length - 1]
      }
    },
    firstNamePrefix(): string {
      return 'prefix ' + this.firstName
    }
  },
  methods: {
    setFullName() {
      this.fullName = '黄 落星'
    }
  }
})
</script>

<style scoped>
a {
  color: #42b983;
}
</style>
