<i18n src="~/locales/components/ClickToCopy.yml"></i18n>

<style lang="scss" scoped>
.copy-input {
  position: relative;
  overflow: hidden;
}
.copy-input input {
  padding-right: 80px; // NOTE: Magic number
  font-family: monospace;
}
.copy-input .btn-copy {
  position: absolute;
  top:    $gutter/2;
  bottom: $gutter/2;
  right:  $gutter/2;
}
</style>

<template>
  <form class="copy-input">
    <button
      @click.prevent
      :data-clipboard-text="textToCopy"
      class="btn btn-sml btn-copy js-clipboard"
      v-text="buttonText">
    </button>

    <input type="text" :value="textToCopy" class="text-input" readonly />
  </form> <!-- .copy-input -->
</template>

<script>
import Clipboard from 'clipboard'

export default {
  props: {
    textToCopy: {
      type: String,
      required: true,
      default: null
    }
  },

  data() {
    return {
      hasRecentlyCopied: false
    }
  },

  computed: {
    buttonText() {
      return this.hasRecentlyCopied ? this.$t('copied_button_text') : this.$t('copy_button_text')
    }
  },

  mounted() {
    const clipboard = new Clipboard('.js-clipboard')
    const self = this
    clipboard.on('success', function (ev) {
      self.successNotification(ev)
      ev.clearSelection()
    })
  },

  methods: {
    successNotification(ev) {
      const self = this
      if (ev.text === this.textToCopy) {
        this.hasRecentlyCopied = true
        setTimeout(function () {
          self.hasRecentlyCopied = false
        }, 2000)
      }
    }
  }
}
</script>
