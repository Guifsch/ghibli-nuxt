<template>
  <v-row class="ma-5">
    <v-col
      v-for="(species, id) in speciesInfo"
      :key="id"
      cols="12"
      md="6"
      lg="4"
      class="d-flex flex-column"
      active-class="primary white--text"
    >
      <v-card class="d-flex flex-column flex-column pa-5">
        <p><span class="sub-title">Name:</span> {{ species.name }}</p>
        <p>
          <span class="sub-title">Classification:</span>
          {{ species.classification }}
        </p>
        <p>
          <span class="sub-title">Eyes color:</span> {{ species.eye_colors }}
        </p>
        <p>
          <span class="sub-title">Hair color:</span> {{ species.hair_colors }}
        </p>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  props: {
    species: {
      type: Array,
      default: () => [],
    },
  },

  data() {
    return {
      speciesInfo: [],
    }
  },

  watch: {
    species: {
      immediate: true,
      handler(species) {
        if (species) {
          this.speciesInfo = []
          this.species.map(async (item) => {
            const param = item.split('/').slice(-1)[0]
            this.speciesInfo.push(await this.$axios.$get(`species/${param}`))
          })
        }
      },
    },
  },
}
</script>
