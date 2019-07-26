<i18n src="~/locales/components/SupporterCloud.yml"></i18n>

<style lang="scss" scoped>
.flex-grid .logo-container {
  display: flex;
  flex: 0 0 30%;
  align-items: center;
  align-content: center;
  justify-content: center;
}
.flex-grid > *:last-child {
  @include respond-to(med) {
    margin-right: $gutter;
  }
}
.flex-grid .logo-container img {
  max-height: 100px;
}

// If Logo Cloud contains people:
.flex-grid.has-people .logo-container {
  min-width: 250px;
}
.flex-grid .logo-container.is-person {
  justify-content: start;
}
</style>

<template>
  <div class="flex-grid sml-flex-col med-flex-row"
       :class="{ 'has-people': hasPeople }">
    <div v-for="(logo, index) in $t('logos')"
        :key="`supporting-org1-${index}`"
        class="fill-white is-rounded sml-pad-1 sml-push-y1 logo-container"
        :class="{ 'is-person': logo.type === 'person' }">
      <img :src="logo.image"
           :alt="logo.name">
      <div v-if="logo.type === 'person'" class="sml-pad-x2">
        <p>{{ logo.name }}</p>
      </div>
    </div> <!-- v-for logo -->
  </div> <!-- .flex-grid -->
</template>

<script>
export default {
  computed: {
    hasPeople() {
      const logosArray = Object.keys(this.$t('logos')).map(i => this.$t('logos')[i])
      return logosArray.findIndex(logo => logo.type === 'person') > -1
    }
  }
}
</script>
