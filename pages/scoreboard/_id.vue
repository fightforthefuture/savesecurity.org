<template>
  <DefaultLayout>
    <section id="sign" class="sml-pad-y3 med-pad-y6">
      <div class="wrapper">
        <nuxt-link to="/scoreboard">&lt; Back to scoreboard</nuxt-link>
        <div class="row sml-push-y2 med-push-y3">
          <div class="sml-c12 lrg-c8 grid-center text-center">
            <h1>
              {{ repOrg }} {{ rep.first_name }} {{ rep.last_name }}
              <span v-text="rep.supports_net_neutrality ? 'Supports' : 'Opposes'"
                :class="{
                  'text-success': rep.supports_net_neutrality,
                  'text-warn': !rep.supports_net_neutrality
                }">
              </span>
              Net Neutrality
            </h1>
            <ScoreboardRep :rep="rep" class="sml-push-y2 med-push-y3" />
          </div> <!-- .c -->
        </div> <!-- .row -->
      </div> <!-- .wrapper -->
    </section>
  </DefaultLayout>
</template>

<script>
import DefaultLayout from '~/components/DefaultLayout'
import ScoreboardRep from '~/components/ScoreboardRep'

export default {
  components: {
    DefaultLayout,
    ScoreboardRep
  },

  head() {
    return {
      titleTemplate: '%s - Scoreboard'
    }
  },

  async asyncData({ $axios, params }) {
    let rep = []
    try {
      const { data } = await $axios.get(`https://data.battleforthenet.com/scoreboard/${params.id}.json`)
      rep = data
    } catch (error) {
      return {}
    }
    return {
      rep: rep
    }
  },

  computed: {
    repOrg() { return this.rep.organization === 'Senate' ? 'Sen. ' : 'Rep.' }
  }
}
</script>
