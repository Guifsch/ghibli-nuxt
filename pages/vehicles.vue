<template>
  <v-row class="ma-5">
    <v-col
      v-for="(vehicles, id) in vehicles"
      :key="id"
      cols="12"
      sm="6"
      md="6"
      lg="4"
      class="d-flex flex-column"
      active-class="primary white--text"
    >
      <v-card class="d-flex flex-column flex-column pa-5">
        <p><span class="sub-title">Name:</span> {{ vehicles.name }}</p>
        <p>
          <span class="sub-title">Description:</span> {{ vehicles.description }}
        </p>
        <p>
          <span class="sub-title">Vehicle class:</span>
          {{ vehicles.vehicle_class }}
        </p>
        <p>
          <span class="sub-title">Vehicle length:</span> {{ vehicles.length }}
        </p>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      vehicles: [],
    }
  },

  mounted() {
    this.allLocations()
  },
  methods: {
    async allLocations() {
      try {
        const content = await this.$axios.$get('vehicles')
        this.vehicles = content
      } catch (e) {
        console.log(e)
      }
    },
  },
}
</script>
