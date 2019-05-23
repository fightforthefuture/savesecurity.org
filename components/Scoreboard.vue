<i18n src="~/locales/components/Scoreboard.yml"></i18n>

<template>
  <div>
    <ScoreboardForm />
    <no-ssr>
      <ScoreboardLegend class="sml-push-y2 med-push-y4" />
      <ScoreboardStateSelect class="sml-push-y2 med-push-y3" />

      <ScoreboardGroup
        v-if="politicians.length > 0"
        :politicians="politicians"
        class="fade-in sml-push-y2" />
      <div v-else-if="selectedState && !isLoading">
        <h3 class="text-center">{{ $t('no_results') }}</h3>
      </div> <!-- v-else-if -->
      <p class="sml-push-y2 med-push-y3 text-center">
        <nuxt-link :to="localePath('scoreboard-all')" class="btn">
          {{ $t('view_all') }}
        </nuxt-link>
      </p>
    </no-ssr>
  </div>
</template>

<script>
import { geocodeState } from '~/assets/js/helpers'
import ScoreboardForm from '~/components/ScoreboardForm'
import ScoreboardGroup from '~/components/ScoreboardGroup'
import ScoreboardLegend from '~/components/ScoreboardLegend'
import ScoreboardStateSelect from '~/components/ScoreboardStateSelect'

export default {
  components: {
    ScoreboardForm,
    ScoreboardGroup,
    ScoreboardLegend,
    ScoreboardStateSelect
  },

  data() {
    return {
      politicians: [],
      isLoading: false
    }
  },

  computed: {
    selectedState: {
      get() {
        return this.$store.state.selectedState
      },
      set(value) {
        this.$store.commit('setSelectedState', value)
      }
    }
  },

  watch: {
    selectedState(newValue) {
      if (!process.browser) return

      if (newValue) {
        localStorage.selectedState = newValue
        this.fetchPoliticians()
      } else {
        localStorage.removeItem('selectedState')
        this.politicians = []
      }
    }
  },

  async created() {
    if (!process.browser) return

    if (localStorage.selectedState) {
      this.selectedState = localStorage.selectedState
    } else {
      const { abbr } = await geocodeState()
      this.selectedState = abbr
    }
  },

  methods: {
    async fetchPoliticians() {
      this.isLoading = true
      this.politicians = []
      const { data } = await this.$axios.get(`https://data.battleforthenet.com/scoreboard/${this.selectedState.toLowerCase()}.json`)
      this.politicians = data
      this.isLoading = false
    }
  }
}
</script>
