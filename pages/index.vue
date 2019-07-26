<i18n src="~/locales/global.yml"></i18n>
<i18n src="~/locales/pages/index.yml"></i18n>

<style lang="scss" scoped>
#intro {
  min-height: 100vh;

  p {
    font-size: $font-size-2;
  }
}

.logo {
  text-align: center;

  img {
    display: block;
    margin: auto;
    width: 300px;
    max-width: 75vw;
  }
}

section:nth-child(odd):not(#intro) {
  background-color: $grey-light-color;
}
</style>

<template>
  <DefaultLayout>
    <section id="intro" class="flex-center">
      <div class="wrapper">
        <div class="row">
          <div class="sml-c12 lrg-c8 grid-center text-center">
            <div class="logo">
              <img src="~/assets/images/lock-bg.png" alt="">
              <h1>{{ $t('global.site_title') }}</h1>
            </div>
            <p>{{ $t('intro') }}</p>

            <ul class="hoz text-center sml-push-y3 med-push-y4">
              <li>
                <a @click.prevent="scrollTo('#sign')">
                  <img src="~assets/images/arrow-down.svg"
                       :alt="$t('scroll_down')" />
                </a>
              </li>
            </ul>
          </div> <!-- .c -->
        </div> <!-- .row -->
      </div> <!-- .wrapper -->
    </section>

    <section v-for="(section, id) in $t('sections')" :id="id" :key="id" class="sml-pad-y3 med-pad-y6">
      <div class="wrapper">
        <div class="row">
          <div class="sml-c12 lrg-c8 grid-center text-center">
            <h2 v-if="section.title">{{ section.title }}</h2>
            <div v-if="section.description_html" class="sml-push-y2 med-push-y3" v-html="section.description_html"></div>
            <ActionNetworkForm v-if="id == 'sign'" />
            <LogoCloud v-if="id == 'coalition'" class="sml-push-y2" />
            <SupporterCloud v-if="id == 'supporters'" class="sml-push-y2" />
          </div> <!-- .c -->
        </div> <!-- .row -->
      </div> <!-- .wrapper -->
    </section>
  </DefaultLayout>
</template>

<script>
import { smoothScrollToElement } from '~/assets/js/helpers'
import DefaultLayout from '~/components/DefaultLayout'
import ActionNetworkForm from '~/components/ActionNetworkForm'
import LogoCloud from '~/components/LogoCloud'
import SupporterCloud from '~/components/SupporterCloud'

export default {
  components: {
    DefaultLayout,
    ActionNetworkForm,
    LogoCloud,
    SupporterCloud
  },

  head() {
    return {
      titleTemplate: `%s - ${this.$t('page_title')}`
    }
  },

  methods: {
    scrollTo(hash) {
      const duration = 500
      smoothScrollToElement(hash, duration)
      setTimeout(() => {
        location.hash = hash
      }, duration)
    }
  }
}
</script>
