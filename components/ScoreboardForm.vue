<template>
  <form @submit.prevent="submitForm()">
    <p class="text-warn" v-if="errorMessage">{{ errorMessage }}</p>
    <div class="flex-grid sml-flex-row">
      <input type="text" v-model="address" placeholder="Street Address*"
             class="sml-flex-2" required>
      <input type="tel" v-model="zipCode" placeholder="ZIP Code*" required>
    </div>
    <button class="btn btn-block sml-push-y1" :disabled="isSending">
      <span v-if="isSending">
        Searching...
      </span>
      <span v-else>
        Let&rsquo;s go!
      </span>
    </button>
    <p class="sml-push-y1">
      <small>
        Your information will only be used to look up your representative.
      </small>
    </p>
  </form>
</template>

<script>
import { fetchRepScoreboard } from '~/assets/js/helpers'

export default {
  data() {
    return {
      isSending: false,
      errorMessage: null
    }
  },

  computed: {
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
    }
  },

  methods: {
    async submitForm() {
      this.$trackEvent('scoreboard_form', 'submit')
      this.isSending = true
      this.errorMessage = null

      try {
        const response = await fetchRepScoreboard({
          street: this.address,
          zip: this.zipCode
        })

        if (response) {
          this.$router.push({
            name: 'scoreboard-id',
            params: {
              id: response.bioguide_id
            }
          })
        }
      } catch (err) {
        this.errorMessage = "Oh no! We couldn't find a representative for your address."
      }

      this.isSending = false
    }
  }
}
</script>
