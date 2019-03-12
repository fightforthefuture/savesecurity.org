<template>
  <StyleguideLayout :component-name="title">
    <p>
      <strong class="text-brand">NOTE:</strong> There are more options than
      those presented here. Please see: <code>_spacing.scss</code>.
    </p>
    <StyleguideBlock :classes="paddingClasses">
      <template v-slot:elem="{ c }">
        <div :class="c" class="fill-white with-border">
          Element with <strong>padding</strong>
        </div>
      </template>
    </StyleguideBlock>

    <StyleguideBlock :classes="marginClasses">
      <template v-slot:elem="{ c }">
        <div :class="c" class="fill-white with-border sml-pad-1">
          Element with <strong>margin</strong>
        </div>
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
      paddingClasses: [
        '',
        'sml-pad-half',
        'sml-pad-1',
        'sml-pad-2',
        'sml-pad-3',
        'sml-pad-4',
        'sml-pad-x1',
        'sml-pad-x2',
        'sml-pad-y1',
        'sml-pad-y2',
        'sml-pad-y4',
        'sml-pad-y6'
      ],
      marginClasses: [
        '',
        'sml-push-y-half',
        'sml-push-y1',
        'sml-push-y2',
        'sml-push-y3',
        'sml-push-y4',
        'sml-push-y5',
        'sml-push-y6'
      ]
    }
  },

  computed: {
    title() { return 'Spacing' }
  }
}
</script>
