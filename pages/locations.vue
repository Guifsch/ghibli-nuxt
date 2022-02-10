<template>
  <v-row class="ma-5">
    <v-col
      v-for="(locations, id) in locations"
      :key="id"
      cols="12"
      sm="6"
      md="6"
      lg="4"
      class="d-flex flex-column"
      active-class="primary white--text"
    >
      <v-card class="d-flex flex-column flex-column pa-5" height="230px">
        <p><span class="sub-title">Name:</span> {{ locations.name }}</p>

        <p v-if="locations.climate === 'TODO'">
          <span class="sub-title">Terrain:</span> No data
        </p>
        <p v-else>
          <span class="sub-title">Terrain:</span> {{ locations.climate }}
        </p>

        <p v-if="locations.terrain === 'TODO'">
          <span class="sub-title">Terrain:</span> No data
        </p>
        <p v-else>
          <span class="sub-title">Terrain:</span> {{ locations.terrain }}
        </p>

        <p v-if="locations.surface_water === ''">
          <span class="sub-title">Surface water:</span> No data
        </p>
        <p v-else>
          <span class="sub-title">Surface water:</span>
          {{ locations.surface_water }}
        </p>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      locations: [],
    }
  },

  mounted() {
    this.allLocations()
  },
  methods: {
    async allLocations() {
      try {
        const content = await this.$axios.$get('locations')
        this.locations = content
      } catch (e) {
        console.log(e)
      }
    },
  },
}
</script>
