<i18n src="~/locales/components/ScoreboardGroup.yml"></i18n>

<style lang="scss" scoped>
.rep {
  display: inline-block;
  margin: $gutter;
}
.rep-link {
  display: block;
  max-width: 100px;
  border: none;
}
</style>

<template>
  <div v-if="politicians.length > 0" class="text-center">
    <div v-for="rep in politicians"
         :key="`rep-${rep.bioguide_id}`"
         class="rep">
      <nuxt-link
          :to="localePath({ name: 'scoreboard-id', params: { id: rep.bioguide_id } })"
          class="rep-link">
        <ScoreboardRep :rep="rep" />
        <div class="btn btn-sml btn-block sml-push-y-half">
          {{ $t('view') }}
        </div>
      </nuxt-link>
    </div> <!-- .rep -->
  </div> <!-- v-if -->
</template>

<script>
import ScoreboardRep from '~/components/ScoreboardRep'

export default {
  components: {
    ScoreboardRep
  },

  props: {
    politicians: {
      type: Array,
      required: true,
      default: null
    }
  }
}
</script>
