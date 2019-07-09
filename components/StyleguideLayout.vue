<style lang="scss" scoped>
.page-header #menu {
  left: auto;
  width: 300px;
  max-width: 90%;
}
</style>

<template>
  <div>
    <header class="page-header">
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
        <input type="checkbox" id="menu-toggle" v-model="checked" />
        <div id="menu" class="sml-pad-2">
          <h2>
            <nuxt-link to="/styleguide/base" @click.native="toggleNav">
              Base
            </nuxt-link>
          </h2>
          <ul>
            <li>
              <nuxt-link to="/styleguide/base#colors" @click.native="toggleNav">
                Colors
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/base#grid" @click.native="toggleNav">
                Grid
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/base#headings" @click.native="toggleNav">
                Headings
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/base#typography" @click.native="toggleNav">
                Typography
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/base#spacing" @click.native="toggleNav">
                Spacing
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/base#modifiers" @click.native="toggleNav">
                Modifiers
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/base#buttons" @click.native="toggleNav">
                Buttons
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/base#forms" @click.native="toggleNav">
                Forms
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/base#lists" @click.native="toggleNav">
                Lists
              </nuxt-link>
            </li>
          </ul>
          <h2 class="sml-push-y2">Components</h2>
          <ul>
            <li>
              <nuxt-link to="/styleguide/ActionNetworkForm" @click.native="toggleNav">
                ActionNetworkForm
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/CallForm" @click.native="toggleNav">
                CallForm
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/Logo" @click.native="toggleNav">
                Logo
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/SocialShareButtons" @click.native="toggleNav">
                SocialShareButtons
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/QuoteScroller" @click.native="toggleNav">
                QuoteScroller
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/LogoCloud" @click.native="toggleNav">
                LogoCloud
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/Map" @click.native="toggleNav">
                Map
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/ClickToCopy" @click.native="toggleNav">
                ClickToCopy
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/Scoreboard" @click.native="toggleNav">
                Scoreboard
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/SelfieForm" @click.native="toggleNav">
                SelfieForm
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/ReadTheLetter" @click.native="toggleNav">
                ReadTheLetter
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/PrintTheLetter" @click.native="toggleNav">
                PrintTheLetter
              </nuxt-link>
            </li>
          </ul>
          <h2 class="sml-push-y2">Modals</h2>
          <ul>
            <li>
              <nuxt-link to="/styleguide/ArchivedModal" @click.native="toggleNav">
                ArchivedModal
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/CallFormModal" @click.native="toggleNav">
                CallFormModal
              </nuxt-link>
            </li>
            <li>
              <nuxt-link to="/styleguide/CallScriptModal" @click.native="toggleNav">
                CallScriptModal
              </nuxt-link>
            </li>
          </ul>
        </div> <!-- #menu -->
      </div> <!-- .c.menu-wrapper -->
    </header>

    <div class="site-content">
      <section class="sml-pad-y5">
        <div class="wrapper">
          <h1>{{ componentName }}</h1>

          <slot />
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
      required: false,
      default: null
    }
  },

  data() {
    return {
      checked: false
    }
  },

  computed: {
    title() { return config.siteTitle },
    pageTitle() { return this.componentName ? `- ${this.componentName}` : '' }
  },

  methods: {
    toggleNav() {
      // NOTE: This respects both the No-JS version where CSS controls the menu
      //       display, and the JS version where clicking on the *currently
      //       active* link needs to close the nav.
      this.checked = !this.checked
    }
  }
}
</script>
