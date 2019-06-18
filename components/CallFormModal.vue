<i18n src="~/locales/components/CallFormModal.yml"></i18n>

<template>
  <div>
    <h2>
      <span class="text-success">{{ $t('thanks' ) }}</span>
      {{ $t('please_call') }}
    </h2>
    <p class="sml-push-y1">{{ $t('instructions' ) }}</p>
    <CallForm />
  </div>
</template>

<script>
import CallForm from '~/components/CallForm'

export default {
  components: {
    CallForm
  }
}
</script>
