<template>
  <div class="countdown-wrapper">
    <h3>Faltam</h3>

    <ul class="timer">
      <li>
        <p>{{ formattedTime.days }}</p>
        dias
      </li>
      <li>
        <p>{{ formattedTime.hours }}</p>
        horas
      </li>
      <li>
        <p>{{ formattedTime.minutes }}</p>
        minutos
      </li>
      <li>
        <p>{{ formattedTime.seconds }}</p>
        segundos
      </li>
    </ul>

    <p class="day">Para o dia {{ day }}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  data() {
    return {
      timer: 0,
      day: this.$route.query.day,
      formattedTime: {
        days: 0,
        hours: 0,
        minutes: 0,
        seconds: 0,
      },
    }
  },

  mounted() {
    const time = Number(this.$route.query.time)
    this.timer = time - new Date().getTime() / 1000
    this.getFormattedTime(this.timer)
  },

  methods: {
    getFormattedTime(timer: number) {
      let formattedTime = this.formattedTime

      formattedTime.days = Math.floor(timer / (60 * 60 * 24))
      formattedTime.hours = Math.floor((timer % (60 * 60 * 24)) / (60 * 60))
      formattedTime.minutes = Math.floor((timer % (60 * 60)) / 60)
      formattedTime.seconds = Math.floor(timer % 60)

      this.formattedTime = formattedTime
      this.timer = this.timer - 1
    },
  },

  watch: {
    'formattedTime.seconds'() {
      setTimeout(() => {
        this.getFormattedTime(this.timer)
      }, 1000)
    },
  },
})
</script>

<style>
.countdown-wrapper {
  margin-top: 2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}

h3 {
  font-size: 2.3rem;
}

ul.timer {
  list-style: none;
  display: flex;
  margin-top: 1rem;
}

ul.timer li {
  display: flex;
  flex-direction: column;
  align-items: center;

  padding: 0 2rem;
  font-size: 1.8rem;
  font-weight: 600;
}

ul.timer p {
  font-size: 2.4rem;
}

p.day {
  font-size: 1.6rem;
  margin-top: 2rem;
}

@media (max-width: 670px) {
  ul.timer li {
    padding: 0 0.5rem;
  }
}

@media (max-width: 500px) {
  ul.timer {
    flex-direction: column;
    padding: 0;
  }

  ul.timer li {
    justify-content: center;
  }
}
</style>
