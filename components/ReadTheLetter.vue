<i18n src="~/locales/components/ReadTheLetter.yml"></i18n>
<i18n src="~/locales/global.yml"></i18n>

<template>
  <div>
    <h2 class="text-center">{{ $t('title') }}</h2>
    <div class="sml-push-y2 med-push-y3" v-html="letterHTML"></div>
  </div>
</template>

<script>
export default {
  props: {
    letter: {
      type: String,
      required: false,
      default: null
    }
  },

  computed: {
    letterHTML() {
      return this.letter ? this.letter : this.$t('global.letter_html')
    }
  }
}
</script>
