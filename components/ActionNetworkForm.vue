<i18n src="~/locales/components/ActionNetworkForm.yml"></i18n>
<i18n src="~/locales/global.yml"></i18n>

<template>
  <div class="sml-push-y2 med-push-y3">
    <div class="text-center">
      <div v-if="hasSigned">
        <h2 class="text-success">{{ $t('thanks.title') }}</h2>
        <p class="sml-push-y1">{{ $t('thanks.share') }}</p>
        <div class="row sml-push-y2 med-push-y3">
          <div class="sml-c12 lrg-c4">
            <ShareButton
              network="twitter"
              class="btn-block"
              :text="tweetText"
              @click.native="$trackClick(`twitter_share_button_success_${routeName}`)">
              <span>{{ $t('global.common.tweet') }}</span>
            </ShareButton>
          </div> <!-- .c -->
          <div class="sml-c12 lrg-c4 sml-push-y1 lrg-push-y0">
            <ShareButton
              network="facebook"
              class="btn-block"
              @click.native="$trackClick(`facebook_share_button_sucess_${routeName}`)">
              <span>{{ $t('global.common.share') }}</span>
            </ShareButton>
          </div> <!-- .c -->
          <div class="sml-c12 lrg-c4 sml-push-y1 lrg-push-y0">
            <a :href="donateUrl"
               class="btn btn-block"
               @click="$trackClick(`donate_button_success_${routeName}`)">
              <span>{{ $t('global.common.donate') }}</span>
            </a>
          </div> <!-- .c -->
        </div> <!-- .row -->
      </div> <!-- v-if -->
    </div> <!-- .push -->
    <form v-if="!hasSigned"
          @submit.prevent="submitForm()">
      <p v-if="errorMessage" class="text-warn">
        {{ errorMessage }}
      </p>
      <div class="flex-grid sml-flex-row">
        <input v-model="name" type="text" :placeholder="$t('form.name')" required>
        <input v-model="email" type="email" :placeholder="$t('form.email')" required>
      </div> <!-- .flex-grid -->
      <div class="flex-grid sml-flex-row sml-push-y1">
        <input v-model="address"
               type="text"
               class="sml-flex-2"
               :placeholder="`${$t('form.address')}${shouldContactCongress === 1 ? '*' : ''}`"
               :required="contactCongress === 1">
        <input v-model="zipCode"
               type="tel"
               :placeholder="$t('form.zip')"
               required>
        <input v-model.trim="phone"
               type="tel"
               class="sml-flex-2"
               :placeholder="$t('form.phone')">
      </div> <!-- .flex-grid -->
      <div v-if="hasCompany" class="sml-push-y1">
        <div v-if="hasCompanyToggle"
             class="flex-grid sml-flex-row flex-center sml-push-y1">
          <p class="sml-flex-2 med-flex-3 text-left">
            {{ $t('form.is_an_org') }}
          </p>
          <div class="radio-toggle sml-pad-half">
            <div class="flex-grid sml-flex-row">
              <div>
                <input
                  v-model="isBusinessOwner"
                  type="radio"
                  :value="false"
                  id="not-biz">
                <label for="not-biz">{{ $t('global.common.no') }}</label>
              </div>
              <div>
                <input
                  v-model="isBusinessOwner"
                  type="radio"
                  :value="true"
                  id="is-biz">
                <label for="is-biz">{{ $t('global.common.yes') }}</label>
              </div>
            </div> <!-- .flex-grid -->
          </div> <!-- .radio-toggle -->
        </div> <!-- .flex-grid -->

        <div v-if="isBusinessOwner || !hasCompanyToggle" class="sml-push-y1">
          <input
            v-model="companyName"
            type="text"
            :placeholder="`${$t('form.company')}${hasCompanyToggle ? '*': ''}`"
            :required="hasCompanyToggle">
        </div> <!-- v-if isBusinessOwner -->
      </div> <!-- v-if hasCompany -->
      <div v-if="hasComment || shouldContactCongress"
           class="sml-push-y1 textarea-with-btn">
        <textarea
          v-model="comment"
          ref="comment"
          :placeholder="$t('form.comment')"
          required>
        </textarea>
        <a class="btn btn-sml btn-alt" @click.prevent="clearComment()">
          {{ $t('global.common.clear') }}
        </a>
      </div> <!-- .textarea-with-btn -->

      <button class="btn btn-block sml-push-y1" :disabled="isSending">
        <span v-if="isSending">{{ $t('global.common.sending') }}</span>
        <span v-else>{{ buttonText }}</span>
      </button>
      <p class="sml-push-y1 text-center">
        <small v-html="$t('privacy_html')"></small>
      </p>
    </form>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import { sendToMothership, startTextFlow } from '~/assets/js/helpers'
import ShareButton from '~/components/ShareButton'

export default {
  components: {
    ShareButton
  },

  props: {
    anPetitionId: {
      type: String,
      required: false,
      default: function () {
        return this.$t('petition_id')
      }
    },
    subject: {
      type: String,
      required: false,
      default: function () {
        return this.$t('subject')
      }
    },
    contactCongress: {
      type: String,
      required: false,
      default: function () {
        return this.$t('contact_congress')
      }
    },
    /* eslint-disable vue/require-prop-types */
    fccDocket: {
      required: false,
      default: function () {
        return this.$te('fcc_docket') ? this.$t('fcc_docket') : null
      }
    },
    callpowerId: {
      required: false,
      default: function () {
        return this.$te('callpower_id') ? this.$t('callpower_id') : null
      }
    },
    /* eslint-enable vue/require-prop-types */
    tags: {
      type: Object,
      required: false,
      default: function () {
        return this.$t('tags')
      }
    },
    textFlowId: {
      type: String,
      required: false,
      default: function () {
        return this.$t('text_flow_id')
      }
    },
    callScript: {
      type: String,
      required: false,
      default: function () {
        return this.$t('global.call_script')
      }
    },
    buttonText: {
      type: String,
      required: false,
      default: function () {
        return this.$t('form.button_cta')
      }
    },
    hasComment: {
      type: Boolean,
      required: false,
      default: false
    },
    hasCompany: {
      type: Boolean,
      required: false,
      default: false
    },
    hasCompanyToggle: {
      type: Boolean,
      required: false,
      default: false
    },
    tweetText: {
      type: String,
      required: false,
      default: null
    },
    letterText: {
      type: String,
      required: false,
      default: function () {
        return this.$t('global.letter_text')
      }
    }
  },

  data() {
    return {
      isSending: false,
      hasSigned: false,
      errorMessage: null,
      comment: null,
      isBusinessOwner: false,
      companyName: null
    }
  },

  computed: {
    ...mapState(['donateUrl']),

    routeName() { return this.$nuxt.$route.name },

    name: {
      get() {
        return this.$store.state.name
      },
      set(value) {
        this.$store.commit('setName', value)
      }
    },

    email: {
      get() {
        return this.$store.state.email
      },
      set(value) {
        this.$store.commit('setEmail', value)
      }
    },

    address: {
      get() {
        return this.$store.state.address
      },
      set(value) {
        this.$store.commit('setAddress', value)
      }
    },

    zipCode: {
      get() {
        return this.$store.state.zipCode
      },
      set(value) {
        this.$store.commit('setZipCode', value)
      }
    },

    phone: {
      get() {
        return this.$store.state.phone
      },
      set(value) {
        this.$store.commit('setPhone', value)
      }
    },

    shouldContactCongress() {
      return this.contactCongress.toLowerCase() === 'yes' ? 1 : 0
    }
  },

  created() {
    this.comment = this.letterText
  },

  methods: {
    async submitForm() {
      if (this.isSending) return

      this.isSending = true

      try {
        const response = await sendToMothership({ // eslint-disable-line no-unused-vars
          subject: this.subject,
          member: {
            first_name: this.name,
            email: this.email,
            phone_number: this.phone,
            street_address: this.address,
            postcode: this.zipCode,
            country: 'US',
            company: this.companyName
          },
          hp_enabled: 'true',
          guard: '',
          contact_congress: this.shouldContactCongress,
          fcc_ecfs_docket: this.fccDocket,
          an_tags: JSON.stringify(Object.values(this.tags)),
          an_petition_id: this.anPetitionId,
          action_comment: this.hasComment ? this.comment : ''
        })

        this.$trackEvent(`petition_form_${this.routeName}`, 'submit')

        if (this.callpowerId) {
          this.$store.commit('setCallpowerCampaignId', this.callpowerId)
          this.$store.commit('setCallScript', this.callScript)
          this.$store.commit('setModalVisibility', true)
          this.$store.commit('setModalType', 'call-form')
        }
        this.isSending = false
        this.hasSigned = true

        if (this.phone) {
          this.startTextFlow()
        }
      } catch (err) {
        this.isSending = false
        this.errorMessage = this.$t('global.common.error')
      }
    },

    clearComment() {
      this.comment = ''
      this.$refs.comment.focus()
    },

    startTextFlow() {
      startTextFlow({
        opt_in_path: this.textFlowId,
        phone: this.phone,
        name: this.name,
        email: this.email,
        zip_code: this.zipCode,
        street: this.address
      })
    }
  }
}
</script>
