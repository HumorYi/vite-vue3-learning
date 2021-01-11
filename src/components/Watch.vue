<template>
  <h1>Watch:</h1>
  <p>
    Ask a yes/no question:
    <input v-model="question" />
  </p>
  <p>{{ answer }}</p>
</template>

<script lang="ts">
import { ref, defineComponent } from 'vue'
import axios from 'axios'

export default defineComponent({
  name: 'Watch',
  data() {
    return {
      question: '',
      answer: 'Questions usually contain a question mark. ;-)'
    }
  },
  emits: ['answer'],
  watch: {
    // whenever question changes, this function will run
    async question(newQuestion: string, oldQuestion: string) {
      if (newQuestion.indexOf('?') > -1) {
        await this.getAnswer()

        this.$emit('answer', newQuestion, this.answer)
      }
    }
  },
  methods: {
    async getAnswer() {
      this.answer = 'Thinking...'

      await axios
        .get('https://yesno.wtf/api')
        .then(response => {
          this.answer = response.data.answer
        })
        .catch(error => {
          this.answer = 'Error! Could not reach the API. ' + error
        })
    }
  }
})
</script>

<style scoped>
a {
  color: #42b983;
}
</style>
