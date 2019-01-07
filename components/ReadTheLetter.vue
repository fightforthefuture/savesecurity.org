<template>
  <div>
    <h2 class="text-center">
Read the Letter
</h2>
    <div class="sml-push-y2 med-push-y3" v-html="letterText" />
  </div>
</template>

<script>
import { simpleFormat } from '~/assets/js/helpers'

export default {
  computed: {
    letterText() { return simpleFormat(this.$store.state.letterText) }
  }
}
</script>
