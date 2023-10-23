<template>
  <div class="mx-auto mt-5">
    <p>Reaction Time: {{ timeTaken }}</p>
    <h3>{{ text }}</h3>
  </div>
</template>

<script>
export default {
  props: ['timeTaken'],
  computed: {
    text() {
      const thresholds = [
        { max: 200, text: 'Sonic Reaction' },
        { max: 300, text: 'Fast Reaction!' },
        { max: 500, text: 'Decent Reaction!' },
        { max: 1000, text: 'Slow Joe' }
      ]

      for (const { max, text } of thresholds) {
        if (this.timeTaken < max) {
          return text
        }
      }

      return 'Snail Pace...'
    }
  }
}
</script>
