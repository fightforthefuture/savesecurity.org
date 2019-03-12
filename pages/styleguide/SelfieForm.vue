<template>
  <StyleguideLayout :component-name="title">
    <h2 class="text-center">Take a photo</h2>

    <SelfieForm />

    <p class="text-center sml-push-y2 med-push-y3">
      <nuxt-link to="/gallery">
        View the gallery
      </nuxt-link>
    </p>
  </StyleguideLayout>
</template>

<script>
import StyleguideLayout from '~/components/StyleguideLayout'
import SelfieForm from '~/components/SelfieForm'

export default {
  components: {
    StyleguideLayout,
    SelfieForm
  },

  computed: {
    title() { return 'SelfieForm' }
  }
}
</script>
