<style lang="scss" scoped>
.politicians {
  text-align: center;
}
.politician {
  display: inline-block;
  margin: $gutter;
}
</style>

<template>
  <no-ssr>
    <div class="politicians">
      <div class="flex-grid sml-flex-row">
        <div class="sml-pad-1 fill-warn">Against</div>
        <div class="sml-pad-1 fill-success">Supports</div>
        <div class="sml-pad-1 fill-grey">No Stance</div>
      </div> <!-- .flex-grid -->

      <select v-model="selectedState" class="sml-push-y2 med-push-y3">
        <option :value="null">Selected state</option>
        <option v-for="(name, code) in states" :key="code" :value="code">{{ name }}</option>
      </select>

      <div v-if="politicians.length > 0" class="fade-in sml-push-y2">
        <div v-for="rep in politicians"
             :key="`rep-${rep.bioguide_id}`"
             class="politician">
          <ScoreboardRep :rep="rep" />
        </div> <!-- .politician -->
      </div> <!-- v-if -->
      <div v-else-if="selectedState && !isLoading">
        <h3>No politicians found</h3>
      </div> <!-- v-else-if -->
      <p class="sml-push-y2 med-push-y3">
        <a href="#TODO" class="btn">View all</a>
      </p>
    </div> <!-- .politicians -->
  </no-ssr>
</template>

<script>
import { geocodeState } from '~/assets/js/helpers'
import US_STATES from '~/data/states.json'
import ScoreboardRep from '~/components/ScoreboardRep'

export default {
  components: {
    ScoreboardRep
  },

  data() {
    return {
      selectedState: null,
      politicians: [],
      isLoading: false
    }
  },

  computed: {
    states() { return US_STATES }
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
