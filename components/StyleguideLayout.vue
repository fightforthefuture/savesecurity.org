<style lang="scss" scoped>
.styleguide-example {
  background: transparentize($grey-light-color, 0.8);
  border: 1px solid $grey-light-color;
  border-radius: $default-border-radius;
}
</style>

<template>
  <div>
    <header class="page-header">
      <div class="wrapper">
        <div class="row">
          <div class="sml-c10 med-c8">
            <nuxt-link to="/styleguide">
              <h2>{{ title }} - Styleguide</h2>
            </nuxt-link>
          </div> <!-- .c -->
          <div class="sml-c2 med-c4 menu-wrapper">
            <label for="menu-toggle" id="menu-label">
              &#9776;
              <span class="text-accessibility">Menu</span>
            </label>
            <input type="checkbox" id="menu-toggle" />
            <div id="menu" class="sml-pad-y2 med-pad-y4">
              <div class="wrapper">
                <div class="row">
                  <div class="sml-c12 med-c4">
                    <h2>Base</h2>
                    <ul>
                      <li>
                        <nuxt-link to="/styleguide/colors">Colors</nuxt-link>
                      </li>
                      <li>
                        <nuxt-link to="/styleguide/grid">Grid</nuxt-link>
                      </li>
                      <li>
                        <nuxt-link to="/styleguide/typography">
                          Typography
                        </nuxt-link>
                      </li>
                      <li>
                        <nuxt-link to="/styleguide/buttons">Buttons</nuxt-link>
                      </li>
                      <li>
                        <nuxt-link to="/styleguide/forms">Forms</nuxt-link>
                      </li>
                      <li>
                        <nuxt-link to="/styleguide/spacing">Spacing</nuxt-link>
                      </li>
                      <li>
                        <nuxt-link to="/styleguide/modifiers">
                          Modifiers
                        </nuxt-link>
                      </li>
                    </ul>
                  </div> <!-- .c -->
                  <div class="sml-c12 med-c4 sml-push-y2 med-push-y0">
                    <h2>Components</h2>
                    <ul>
                      <li>
                        <nuxt-link to="/styleguide/ActionNetworkForm">
                          ActionNetworkForm
                        </nuxt-link>
                      </li>
                    </ul>
                  </div> <!-- .c -->
                  <div class="sml-c12 med-c4 sml-push-y2 med-push-y0">
                    <!-- TBD -->
                  </div> <!-- .c -->
                </div> <!-- .row -->
              </div> <!-- .wrapper -->
            </div> <!-- #menu -->
          </div> <!-- .c.menu-wrapper -->
        </div> <!-- .row -->
      </div> <!-- .wrapper -->
    </header>

    <div class="site-content">
      <section class="sml-pad-y5">
        <div class="wrapper">
          <h1>{{ componentName }}</h1>

          <div class="styleguide-example sml-pad-2 sml-push-y2 med-push-y4">
            <slot />
          </div> <!-- .styleguide example -->
        </div> <!-- .wrapper -->
      </section>
    </div> <!-- .site-content -->
  </div>
</template>

<script>
import config from '~/config'

export default {
  head() {
    return {
      titleTemplate: `%s - Styleguide ${this.pageTitle}`
    }
  },

  props: {
    componentName: {
      type: String,
      required: true,
      default: null
    }
  },

  computed: {
    title() { return config.siteTitle },
    pageTitle() { return this.componentName ? `- ${this.componentName}` : '' }
  }
}
</script>
