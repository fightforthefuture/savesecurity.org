<i18n src="~/locales/components/ScoreboardStateSelect.yml"></i18n>

<template>
  <select v-model="selectedState">
    <option :value="null">{{ $t('select_state') }}</option>
    <option v-for="(name, code) in states" :key="code" :value="code">
      {{ name }}
    </option>
  </select>
</template>

<script>
import US_STATES from '~/assets/data/states.json'

export default {
  computed: {
    states() { return US_STATES },
    selectedState: {
      get() {
        return this.$store.state.selectedState
      },
      set(value) {
        this.$store.commit('setSelectedState', value)
      }
    }
  }
}
</script>
