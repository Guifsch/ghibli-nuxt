<template>
  <v-row
    align="center"
    justify="center"
    :class="{
      'ma-0': $vuetify.breakpoint.smAndDown,
      'ma-5': $vuetify.breakpoint.mdAndUp,
    }"
  >
    <v-col cols="2" class="d-none d-md-flex" />

    <v-col class="d-flex" sm="12" md="8">
      <v-img
        :src="require('../assets/studio_ghibli.jpg')"
        :lazy-src="require('../assets/studio_ghibli.jpg')"
      />
    </v-col>

    <v-col cols="2" class="d-none d-md-flex" />

    <v-col cols="1" class="d-none d-md-flex" />
    <v-col sm="12" md="10">
      <p class="font-size">
        <span class="sub-title">Studio Ghibli Inc.</span> Is a
        <span class="sub-title">Japanese animation film studio</span>
        headquartered in Koganei, Tokyo. The studio is best known for its
        <span class="sub-title">animated feature films</span>, and has also
        produced several short subjects, television commercials, and one
        television film. The studio's mascot and most recognizable symbol is a
        character named <span class="sub-title">Totoro</span>, who is a giant
        catlike spirit from the 1988 anime film
        <span class="sub-title">My Neighbor Totoro</span>. Among Studio Ghibli's
        highest-grossing films are
        <span class="sub-title">Spirited Away (2001</span>),
        <span class="sub-title">Howl's Moving Castle (2004)</span> and
        <span class="sub-title">Ponyo (2008</span>). The studio was founded on
        <span class="sub-title">June 15, 1985</span>, by directors
        <span class="sub-title">Hayao Miyazaki</span> and
        <span class="sub-title">Isao Takahata</span> and producer
        <span class="sub-title">Toshio Suzuki</span>, after the successful
        performance of
        <span class="sub-title"
          >Topcraft's Nausicaä of the Valley of the Wind (1984)</span
        >. It has also collaborated with video game studios on the visual
        development of <span class="sub-title">several video games</span>.
      </p>
    </v-col>

    <v-col cols="1" offset class="d-none d-md-flex" />
  </v-row>
</template>

<script>
export default {}
</script>
<style scoped>
.font-size {
  font-size: 1.3rem;
  text-align: justify;
}
</style>
