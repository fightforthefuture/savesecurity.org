<style lang="scss" scoped>
.styleguide-class-tag {
  padding: 2px 5px;
  background: $white;
  border: 1px solid $grey-color;
  border-radius: $default-border-radius;
  font-family: monospace;
}
</style>

<template>
  <div>
    <div v-for="(c, index) in classes"
         :key="`type-class-${c}`"
         class="sml-pad-y2"
         :class="{ 'with-border-bottom': index < classes.length-1 }">
      <p>
        <span class="styleguide-class-tag"
              v-text="c ? `.${c.replace(' ', '.')}` : 'Default'">
        </span>
      </p>
      <div class="sml-push-y-half">
        <slot name="elem" :c="c" />
      </div> <!-- .push -->
    </div> <!-- .with-border -->
  </div>
</template>

<script>
export default {
  props: {
    classes: {
      type: Array,
      required: true,
      default: null
    }
  }
}
</script>
