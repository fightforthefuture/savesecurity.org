<template>
  <StyleguideLayout component-name="ClickToCopy">
    <StyleguideExample>
      <ClickToCopy text-to-copy="Copy me!" />
    </StyleguideExample>
  </StyleguideLayout>
</template>

<script>
import StyleguideLayout from '~/components/StyleguideLayout'
import StyleguideExample from '~/components/StyleguideExample'
import ClickToCopy from '~/components/ClickToCopy'

export default {
  components: {
    StyleguideLayout,
    StyleguideExample,
    ClickToCopy
  }
}
</script>
