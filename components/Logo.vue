<template>
  <h2>{{ title }}</h2>
</template>

<script>
import config from '~/config'

export default {
  computed: {
    title() { return config.siteTitle }
  }
}
</script>
