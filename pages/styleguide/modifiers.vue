<template>
  <StyleguideLayout :component-name="title">
    <p>
      <strong class="text-brand">NOTE:</strong> There are more options than
      those presented here. Please see: <code>_modifiers.scss</code>.
    </p>

    <StyleguideBlock :classes="classes">
      <template v-slot:elem="{ c }">
        <div :class="c" class="sml-pad-2">Element with modifier</div>
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
        'fill-white',
        'fill-grey',
        'fill-brand',
        'with-border',
        'with-border-bottom',
        'with-border-top',
        'with-border is-rounded',
        'with-border is-rounded-top',
        'with-border is-rounded-bottom'
      ]
    }
  },

  computed: {
    title() { return 'Modifiers' }
  }
}
</script>
