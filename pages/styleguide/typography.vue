<template>
  <StyleguideLayout :component-name="title">
    <h1>Heading 1</h1>
    <h2>Heading 2</h2>
    <h3>Heading 3</h3>
    <h4>Heading 4</h4>
    <h5>Heading 5</h5>
    <h6>Heading 6</h6>

    <StyleguideBlock :classes="classes" class="sml-push-y2 med-push-y4">
      <template v-slot:elem="{ c }">
        <p :class="c">
          This is some text <strong>in bold</strong> and <em>emphasized</em>,
          <a href="#">with a link</a>.
        </p>
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
        'text-loud',
        'text-center',
        'text-right',
        'text-left',
        'text-white',
        'text-meta',
        'text-brand',
        'text-warn',
        'text-success'
      ]
    }
  },

  computed: {
    title() { return 'Typography' }
  }
}
</script>
