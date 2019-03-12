<template>
  <StyleguideLayout :component-name="title">
    <Map :events="events" />
  </StyleguideLayout>
</template>

<script>
import StyleguideLayout from '~/components/StyleguideLayout'
import Map from '~/components/Map'

export default {
  components: {
    StyleguideLayout,
    Map
  },

  async asyncData({ $axios }) {
    let events = []
    try {
      const { data } = await $axios.get('https://data.battleforthenet.com/events.json')

      events = data.filter(e => e.category === 'facebook_group').sort((a, b) => {
        if (a.address < b.address) {
          return -1
        } else if (a.address > b.address) {
          return 1
        } else {
          return 0
        }
      })
    } catch (error) {
      //
    } return {
      events: events
    }
  },

  computed: {
    title() { return 'Map' }
  }
}
</script>
