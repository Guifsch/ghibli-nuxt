<template>
  <v-row class="ma-5">
    <v-col
      v-for="(vehicles, id) in vehiclesInfo"
      :key="id"
      cols="12"
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
  props: {
    vehicles: {
      type: Array,
      default: () => [],
    },
  },

  data() {
    return {
      vehiclesInfo: [],
    }
  },

  watch: {
    vehicles: {
      immediate: true,
      handler(vehicles) {
        if (vehicles) {
          this.vehiclesInfo = []
          this.vehicles.map(async (item) => {
            const param = item.split('/').slice(-1)[0]
            this.vehiclesInfo.push(await this.$axios.$get(`vehicles/${param}`))
          })
        }
      },
    },
  },
}
</script>
