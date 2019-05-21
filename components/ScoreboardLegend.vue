<i18n src="~/locales/components/ScoreboardLegend.yml"></i18n>

<template>
  <div class="flex-grid sml-flex-row text-center">
    <div class="sml-pad-1 fill-warn">{{ $t('against') }}</div>
    <div class="sml-pad-1 fill-success">{{ $t('supports') }}</div>
    <div class="sml-pad-1 fill-grey">{{ $t('no_stance') }}</div>
  </div> <!-- .flex-grid -->
</template>
