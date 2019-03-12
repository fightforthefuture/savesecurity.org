<style lang="scss" scoped>
.styleguide-color {
  width:  80px;
  height: 80px;
}
</style>

<template>
  <StyleguideLayout :component-name="title">
    <StyleguideBlock :classes="classes">
      <template v-slot:elem="{ c }">
        <div :class="c" class="styleguide-color"><!-- empty divs are usually evil --></div>
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
        'fill-white',
        'fill-grey-light',
        'fill-grey',
        'fill-grey-dark',
        'fill-black',
        'fill-brand',
        'fill-brand-dark',
        'fill-success',
        'fill-warn'
      ]
    }
  },

  computed: {
    title() { return 'Colors' }
  }
}
</script>
