<template>
  <v-row class="ma-5">
    <v-col
      v-for="(people, id) in people"
      :key="id"
      cols="12"
      sm="6"
      md="6"
      lg="4"
      class="d-flex flex-column"
      active-class="primary white--text"
    >
      <v-card class="d-flex flex-column flex-column pa-5" height="230px">
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
  data() {
    return {
      people: [],
    }
  },

  mounted() {
    this.allPeople()
  },
  methods: {
    async allPeople() {
      try {
        const content = await this.$axios.$get('people')
        this.people = content
      } catch (e) {
        console.log(e)
      }
    },
  },
}
</script>
