<template>
  <v-row class="ma-5">
    <v-col
      v-for="(people, id) in peopleInfo"
      :key="id"
      cols="12"
      sm="6"
      md="6"
      lg="4"
      class="d-flex flex-column"
      active-class="primary white--text"
    >
      <v-card class="d-flex flex-column flex-column pa-5">
        <p><span class="sub-title">Name:</span> {{ people.name }}</p>
        <p><span class="sub-title">Gender:</span> {{ people.gender }}</p>
        <p><span class="sub-title">Age:</span> {{ people.age }}</p>
        <p><span class="sub-title">Gender:</span> {{ people.eye_color }}</p>
        <p><span class="sub-title">Age:</span> {{ people.hair_color }}</p>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  props: {
    people: {
      type: Array,
      default: () => [],
    },
  },

  data() {
    return {
      peopleInfo: [],
      peopleFilm: [],
      filmUrl: [],
      teste: null,
    }
  },

  watch: {
    people: {
      immediate: true,
      handler(people) {
        if (people) {
          this.peopleInfo = []
          this.people.map(async (item) => {
            const param = item.split('/').slice(-1)[0]

            this.peopleInfo.push(await this.$axios.$get(`people/${param}`))
          })
        }
      },
    },
  },

  methods: {},
}
</script>
