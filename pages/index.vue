<template>
  <DefaultLayout>
    <section class="sml-pad-y3 med-pad-y6 sml-pad-y-top2">
      <div class="wrapper">
        <div class="row">
          <div class="sml-c12 lrg-c8 grid-center text-center">
            <p>
              Sub heading goes here, lorem ipsum dolor sit amet, consectetur
              adipiscing elit. In nibh libero, venenatis sed justo eu,
              sollicitudin sollicitudin nisi. Integer semper tortor orci,
              id ultricies velit laoreet in. Vestibulum sit amet ante vel risus
              ornare ultrices sed id leo.
            </p>
            <a class="btn btn-block sml-push-y2 med-push-y3" href="#TODO">
              Call to action
            </a>

            <ul class="hoz sml-push-y2 med-push-y3">
              <li>
                <a @click.prevent="scrollTo('#sign')">
                  Sign the petition
                </a>
              </li>
            </ul>
          </div> <!-- .c -->
        </div> <!-- .row -->
      </div> <!-- .wrapper -->
    </section>

    <section id="sign" class="sml-pad-y3 med-pad-y6 fill-grey-light">
      <div class="wrapper">
        <div class="row">
          <div class="sml-c12 lrg-c8 grid-center text-center">
            <h2>Sign the petition</h2>
            <ActionNetworkForm />
          </div> <!-- .c -->
        </div> <!-- .row -->
      </div> <!-- .wrapper -->
    </section>

    <SocialSidebar />
  </DefaultLayout>
</template>

<script>
import config from '~/config'
import { createMetaTags, smoothScrollToElement } from '~/assets/js/helpers'
import DefaultLayout from '~/components/DefaultLayout'
import ActionNetworkForm from '~/components/ActionNetworkForm'
import SocialSidebar from '~/components/SocialSidebar'

export default {
  components: {
    DefaultLayout,
    ActionNetworkForm,
    SocialSidebar
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
