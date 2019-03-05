<template>
  <StyleguideLayout>
    <h1>{{ title }}</h1>
    <component :is="componentInstance" class="sml-push-y2 med-push-y4"></component>
  </StyleguideLayout>
</template>

<script>
import StyleguideLayout from '~/components/StyleguideLayout'

export default {
  components: {
    StyleguideLayout
  },

  head() {
    return {
      titleTemplate: `%s - Styleguide - ${this.id}`
    }
  },

  computed: {
    id() {
      return this.$route.params.id
    },
    title() {
      return `${this.id.charAt(0).toUpperCase()}${this.id.slice(1)}`
    },
    componentInstance() {
      return () => import(`~/components/${this.id}`)
    }
  }
}
</script>
