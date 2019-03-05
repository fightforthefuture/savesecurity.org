<template>
  <div>
    <h1>Heading 1</h1>
    <h2>Heading 2</h2>
    <h3>Heading 3</h3>
    <h4>Heading 4</h4>
    <h5>Heading 5</h5>
    <h6>Heading 6</h6>

    <p v-for="c in classes"
       :key="`type-class-${c}`"
       class="sml-push-y2"
       :class="c">
      This is some text <strong>in bold</strong> and <em>emphasized</em>,
      <a href="#">with a link</a>.
    </p>
  </div>
</template>

<script>
export default {
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
  }
}
</script>
