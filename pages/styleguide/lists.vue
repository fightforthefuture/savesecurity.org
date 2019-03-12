<template>
  <StyleguideLayout :component-name="title">
    <StyleguideBlock :classes="classes">
      <template v-slot:elem="{ c }">
        <ul :class="c">
          <li>Item 1</li>
          <li><a href="#">Item 2 link</a></li>
          <li>Item 3</li>
        </ul>
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
        'bullets',
        'numbers',
        'hoz'
      ]
    }
  },

  computed: {
    title() { return 'Lists' }
  }
}
</script>
