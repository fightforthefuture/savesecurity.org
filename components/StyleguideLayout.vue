<template>
  <div>
    <header class="page-header">
      <div class="wrapper">
        <div class="row">
          <div class="sml-c6 med-c8">
            <nuxt-link to="/styleguide">
              <h2>{{ title }} - Styleguide</h2>
            </nuxt-link>
          </div> <!-- .c -->
          <div class="sml-c6 med-c4">
            <ul class="hoz sml-push-y-half">
              <li><nuxt-link to="/styleguide/grid">Grid</nuxt-link></li>
              <li><nuxt-link to="/styleguide/typography">Typography</nuxt-link></li>
              <li><nuxt-link to="/styleguide/ActionNetworkForm">ActionNetworkForm</nuxt-link></li>
            </ul> <!-- .flex-grid -->
          </div> <!-- .c -->
        </div> <!-- .row -->
      </div> <!-- .wrapper -->
    </header>

    <div class="site-content">
      <section class="sml-pad-y5">
        <div class="wrapper">
          <slot />
        </div> <!-- .wrapper -->
      </section>
    </div> <!-- .site-content -->
  </div>
</template>

<script>
import config from '~/config'

export default {
  computed: {
    title() { return config.siteTitle }
  }
}
</script>
