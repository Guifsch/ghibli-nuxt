<template>
  <v-dialog :value="dialog" @click:outside="$emit('fechar')">
    <v-card class="pt-3 pr-3">
      <v-toolbar-items>
        <v-spacer />
        <v-btn text small @click="$emit('fechar')">
          <v-icon>mdi-close</v-icon>
        </v-btn>
      </v-toolbar-items>
    </v-card>

    <v-tabs v-model="tab" fixed-tabs color="#1effff">
      <v-tab href="#one"> Film </v-tab>
      <v-tab href="#two" :disabled="disabledPeople"> People </v-tab>
      <v-tab href="#three" :disabled="disabledSpecies"> Species </v-tab>
      <v-tab href="#four" :disabled="disabledVehicles"> Vehicles </v-tab>
    </v-tabs>

    <v-tabs-items v-model="tab">
      <v-tab-item value="one">
        <v-card v-if="film" class="pa-5">
          <v-row>
            <v-col
              cols="12"
              sm="12"
              md="4"
              lg="4"
              class="d-flex flex-column align-center"
            >
              <h1 class="title-size">{{ film.title }}</h1>
              <h1 class="pb-3 title-size">{{ film.original_title }}</h1>
              <v-img :src="film.image" class="img-width" />
            </v-col>
            <v-col cols="12" sm="12" md="8" lg="8">
              <h3 class="text-center sub-title">Description</h3>
              <p>{{ film.description }}</p>
              <h3 class="text-center sub-title">Producer</h3>
              <p class="text-center">{{ film.producer }}</p>
              <h3 class="text-center sub-title">Release date</h3>
              <p class="text-center">{{ film.release_date }}</p>
              <h3 class="text-center sub-title">Running time</h3>
              <p class="text-center">{{ film.running_time }}</p>
              <h3 class="text-center sub-title">Rt score</h3>
              <p class="text-center">{{ film.rt_score }}</p>
            </v-col>
          </v-row>
        </v-card>
        <v-card v-else> Error Data </v-card>
      </v-tab-item>

      <v-tab-item value="two">
        <People :people="people" />
      </v-tab-item>
      <v-tab-item value="three">
        <Species :species="species" />
      </v-tab-item>
      <v-tab-item value="four">
        <Vehicles :vehicles="vehicles" />
      </v-tab-item>
    </v-tabs-items>
  </v-dialog>
</template>

<script>
export default {
  components: {
    People: () => import('./DialogPeople'),
    Species: () => import('./DialogSpecies'),
    Vehicles: () => import('./DialogVehicles'),
  },
  props: {
    dialog: {
      type: Boolean,
      default: false,
    },
    film: {
      type: Object,
      default: () => {},
    },
  },

  data() {
    return {
      tab: 'one',
      people: [],
      species: [],
      vehicles: [],
      peopleEmpty: null,
      paramPeople: null,
      paramSpecies: null,
      disabledPeople: false,
      disabledSpecies: false,
      disabledVehicles: false,
    }
  },

  watch: {
    film: {
      immediate: true,
      handler(film) {
        if (film) {
          this.tab = 'one'
          this.people = this.film.people
          this.species = this.film.species
          this.vehicles = this.film.vehicles

          this.film.people.map((item) => {
            return (this.paramPeople = item.split('/').slice(-1)[0])
          })

          this.film.species.map((item) => {
            return (this.paramSpecies = item.split('/').slice(-1)[0])
          })

          this.film.vehicles.map((item) => {
            return (this.paramVehicles = item.split('/').slice(-1)[0])
          })

          if (this.paramPeople.length === 0) {
            this.disabledPeople = true
          } else {
            this.disabledPeople = false
          }
          if (this.paramSpecies.length === 0) {
            this.disabledSpecies = true
          } else {
            this.disabledSpecies = false
          }
          if (this.paramVehicles.length === 0) {
            this.disabledVehicles = true
          } else {
            this.disabledVehicles = false
          }
        }
      },
    },
  },
}
</script>
<style scoped>
.title-size {
  font-size: 2rem;
}

.img-width {
  width: 70%;
}

@media (max-width: 991.98px) {
  .img-width {
    width: 50%;
  }
}

@media (max-width: 576px) {
  .img-width {
    width: 100%;
  }

  .title-size {
    font-size: 1.2rem;
  }
}
</style>
