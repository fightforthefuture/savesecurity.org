<template>
  <StyleguideLayout :component-name="title">
    <StyleguideBlock :classes="classes">
      <template v-slot:elem="{ c }">
        <a class="btn" :class="c">Button Link</a>
        <button class="btn" :class="c">Button</button>
      </template>
    </StyleguideBlock>
  </StyleguideLayout>
</template>

<script>
import StyleguideLayout from '~/components/StyleguideLayout'
import StyleguideBlock from '~/components/StyleguideBlock'

export default {
  components: {
    StyleguideLayout,
    StyleguideBlock
  },

  data() {
    return {
      classes: [
        '',
        'btn-block',
        'btn-sml',
        'btn-twitter',
        'btn-facebook',
        'btn-disabled'
      ]
    }
  },

  computed: {
    title() { return 'Buttons' }
  }
}
</script>
