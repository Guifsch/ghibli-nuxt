<template>
  <v-row align="center">
    <Dialog :film="film" :dialog="dialog" @fechar="dialog = false" />

    <v-col v-for="(item, i) in films" :key="i" cols="12" sm="6" md="6" lg="4">
      <v-card :color="item.color" dark @click="filmData(item)">
        <v-img :src="item.image" :lazy-src="item.image"><span></span></v-img>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  components: {
    Dialog: () => import('../components/dialog/Dialog'),
  },
  data() {
    return {
      films: null,
      film: null,
      dialog: false,
    }
  },

  mounted() {
    this.allFilms()
  },
  methods: {
    async allFilms() {
      try {
        const content = await this.$axios.$get('films')
        this.films = content
      } catch (e) {
        console.log(e)
      }
    },
    filmData(item) {
      this.dialog = true
      this.film = item
    },
  },
}
</script>
