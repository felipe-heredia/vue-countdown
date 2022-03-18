<script lang="ts">
import { defineComponent } from 'vue'
import { maska } from 'maska'

export default defineComponent({
  data() {
    return {
      dateInput: '',
      showError: false,
    }
  },

  methods: {
    showCountdown() {
      this.showError = false
      const inputData = this.dateInput
      const time = inputData.split('/').reverse().join('-')
      const parsedDateInSeconds = Date.parse(time) / 1000

      if (!parsedDateInSeconds) {
        this.showError = true
      }

      this.$router.push(`/countdown?time=${parsedDateInSeconds}&day=${inputData}`)
    },
  },

  directives: { maska },
})
</script>

<template>
  <form class="get-date" @submit.prevent="showCountdown">
    <h3>Informe uma data</h3>

    <span class="error" v-show="showError">Informe uma data válida!</span>

    <input
      type="text"
      v-model="dateInput"
      class="date-input"
      placeholder="DD/MM/AAAA"
      v-maska="'##/##/####'"
      required
    />

    <button type="submit" class="show-countdown">Ver contagem regressiva</button>
  </form>
</template>

<style>
.get-date {
  display: flex;
  flex-direction: column;
  align-items: center;
}

h3 {
  font-size: 1.8rem;
  font-weight: 600;
}

span.error {
  font-size: 1rem;
  color: #c63030;
}

.date-input {
  background: var(--color-background-mute);
  color: var(--color-text);
  padding: 0.6rem 1.6rem;
  font-size: 2rem;
  border: none;
  border-radius: 1rem;
  margin-top: 2rem;
}

.date-input:focus {
  outline: 2px solid var(--vt-c-white-mute);
}

button.show-countdown {
  margin-top: 2rem;
  padding: 1rem 2rem;
  font-size: 1.2rem;
  border-radius: 1rem;
  background: var(--vt-c-indigo);
  color: var(--vt-c-text-dark-1);
  border: none;
  transition: all 1s;
  cursor: pointer;
}

button.show-countdown:hover {
  background: var(--vt-c-indigo-lighten);
  border-radius: 1.3rem;
}

@media (max-width: 520px) {
  h3 {
    font-size: 1.5rem;
  }

  .date-input {
    font-size: 1.6rem;
  }
}
</style>
