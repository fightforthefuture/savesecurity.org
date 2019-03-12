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
              <li v-for="s in sections" :key="`link-${s}`">
                <nuxt-link :to="{ path: `/styleguide/${s}` }">{{ s }}</nuxt-link>
              </li>
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
  data() {
    return {
      sections: [
        'grid',
        'typography',
        'ActionNetworkForm'
      ]
    }
  },

  computed: {
    title() { return config.siteTitle }
  }
}
</script>
