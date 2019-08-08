<i18n src="~/locales/global.yml"></i18n>
<i18n src="~/locales/pages/index.yml"></i18n>

<style lang="scss" scoped>
$item-width: 15rem;
$item-padding: 2rem;

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

.gallery {
  width: 90%;
  max-width: ($item-width + $item-padding) * 3;
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
  margin: 2rem auto 4rem;

  .item {
    background-color: $grey-light-color;
    border-bottom: none;
    width: $item-width;
    height: $item-width;
    margin: 1rem;
    padding: 3rem;
    border-radius: 16px;
    position: relative;
    color: inherit;

    label {
      position: absolute;
      top: 1rem;
      left: $item-padding;
      right: $item-padding;
      font-size: 1.2rem;
      width: $item-width - ($item-padding * 2);
    }

    img {
      max-width: $item-width * .45;
      max-height: $item-width * .45;
      margin-bottom: 3rem;
      margin-top: 1rem;
    }

    .btn {
      background-color: $grey-dark-color;
      border-radius: 16px;
      font-size: .7rem;
      position: absolute;
      bottom: 1.2rem;
      left: $item-padding;
      right: $item-padding;
      padding: 1rem;
      display: flex;
      justify-content: center;
      align-items: center;

      &:after {
        content: "";
        background-image: url('~assets/images/download.svg');
        background-size: 100% auto;
        background-repeat: no-repeat;
        height: 1rem;
        width: 1rem;
        margin-left: 0.5rem;
      }
    }

    &:hover {
      cursor: pointer;
      background-color: lighten($grey-light-color, 2%);
      transform: scale(1.02);
      transition: background-color .3s, transform .2s;

      .btn {
        background-color: lighten($grey-dark-color, 10%);
        transition: background-color .2s;
      }
    }
  }
}

section:nth-child(odd):not(#intro) {
  background-color: $grey-light-color;

  .gallery .item {
    background-color: $white;

    &:hover {
      background-color: $white;
    }
  }
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
          <div class="sml-c12 grid-center text-center" v-bind:class="{'lrg-c8': (id != 'social')}">
            <h2 v-if="section.title">{{ section.title }}</h2>
            <div v-if="section.description_html" class="sml-push-y2 med-push-y3" v-html="section.description_html" v-bind:class="{'lrg-c8 grid-center': (id == 'social')}"></div>
            <ActionNetworkForm v-if="id == 'sign'" />
            <LogoCloud v-if="id == 'coalition'" class="sml-push-y2" />
            <SupporterCloud v-if="id == 'supporters'" class="sml-push-y2" />
            <div v-if="id == 'social'" class="gallery">
              <a v-for="image in galleries[id]" :key="image" class="item flex-center" :href="image" target="_blank" @click="$trackClick(id + '_image_gallery', image.split('/').pop())">
                <label class="truncate">{{ imageLabel(image) }}</label>
                <img :src="`${image}`" :alt="image">
                <span class="btn">{{ $t('download_button') }}</span>
              </a>
            </div>
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
import galleries from '~/assets/data/media'

export default {
  components: {
    DefaultLayout,
    ActionNetworkForm,
    LogoCloud,
    SupporterCloud
  },

  computed: {
    galleries: () => galleries
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
    },

    imageLabel(image) {
      return image.split('/').pop().split('@')[0].replace(/\.(png|jpg|jpeg|gif)$/i, '')
    }
  }
}
</script>
