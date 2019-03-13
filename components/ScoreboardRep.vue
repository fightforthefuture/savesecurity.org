<style lang="scss" scoped>
.rep-link {
  display: block;
  max-width: 100px;
  border: none;
}
.rep-photo {
  position: relative;
  overflow: hidden;
}
.rep-photo img {
  filter: grayscale(100%); // NOTE: limited browser support
}
.rep-photo:before {
  content: '';
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 10;
  background: rgba(100,100,100, 0.5);
}
.rep-photo.vote-yes:before {
  background: linear-gradient(90deg, #37bfa4, #3576ad);
  opacity: 0.5;
}
.rep-photo.vote-no:before {
  background: rgba(255,26,9,.5);
}
.rep-photo .rep-name {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: $gutter/2;
  z-index: 100;
  text-align: center;
  text-shadow: 0 0 5px $black;
}
</style>

<template>
  <a href="#TODO" class="rep-link">
    <div class="rep-photo is-rounded"
      :class="{
        'vote-yes': rep.supports_net_neutrality === true,
        'vote-no': rep.supports_net_neutrality === false
      }">
      <img :src="`https://congress-photos.fightforthefuture.org/225x275/${rep.bioguide_id}.jpg`"
           :alt="`Photo of ${subtitle} ${fullName}`">
      <h5 class="rep-name text-white">
        {{ rep.last_name }}
        <small>{{ subtitle }}</small>
      </h5>
    </div> <!-- .rep-photo -->
    <div class="btn btn-sml btn-block sml-push-y-half">View</div>
  </a>
</template>

<script>
export default {
  props: {
    rep: {
      type: Object,
      required: true,
      default: null
    }
  },

  computed: {
    subtitle() {
      const org = this.rep.organization === 'Senate' ? 'SEN ' : ''
      const party = this.rep.party ? this.rep.party.substr(0, 1).toUpperCase() : ''
      return `(${org}${party} - ${this.rep.state})`
    },

    fullName() {
      return `${this.rep.first_name} ${this.rep.last_name}`
    }
  }
}
</script>
