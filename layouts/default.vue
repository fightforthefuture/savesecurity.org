<template>
  <div>
    <nuxt />

    <Modal>
      <CallFormModal v-if="modalType === 'call-form'" />
      <CallScriptModal v-if="modalType === 'call-script'" />
      <SelfieModal v-if="modalType === 'selfie'" :selfie="modalData" />
      <ArchivedModal v-if="modalType === 'archived'" />
    </Modal>
  </div>
</template>

<script>
import config from '~/config'
import { mapState } from 'vuex'
import { createMetaTags } from '~/assets/js/helpers'
import Modal from '~/components/Modal'
import CallFormModal from '~/components/CallFormModal'
import CallScriptModal from '~/components/CallScriptModal'
import SelfieModal from '~/components/SelfieModal'
import ArchivedModal from '~/components/ArchivedModal'

export default {
  components: {
    Modal,
    CallFormModal,
    CallScriptModal,
    SelfieModal,
    ArchivedModal
  },

  head() {
    return {
      title: config.siteTitle,
      meta: createMetaTags({
        siteName: config.siteTitle,
        title: config.sharing.title,
        description: config.sharing.description,
        image: config.sharing.image,
        url: config.sharing.url
      })
    }
  },

  computed: {
    ...mapState(['modalType', 'modalData'])
  }
}
</script>
