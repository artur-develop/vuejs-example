<template>
  <div v-if="!loading">
    <v-container fluid>
      <v-layout row>
        <v-flex xs12>
          <v-carousel>
            <v-carousel-item
              v-for="ad in promoAds"
              :key="ad.id"
              :src="ad.imageSrc"
              reverse-transition="fade-transition"
              transition="fade-transition"
            >
              <div class="ad-link">
                <v-btn class="error" :to="'/ad/' + ad.id">{{ad.title}}</v-btn>
              </div>
            </v-carousel-item>
          </v-carousel>
        </v-flex>
      </v-layout>
    </v-container>
    <v-container grid-list-lg>
      <v-layout row wrap>
        <v-flex
          xs12
          md4
          sm6
          v-for="(ad, i) of ads"
          :key="ad.id"
        >
          <v-card
            class="mx-auto"
            max-width="400"
          >
            <v-img
              class="white--text align-end"
              height="200px"
              :src="ad.imageSrc"
            >
              <v-card-title>{{ad.title}}</v-card-title>
            </v-img>

            <v-card-subtitle class="pb-0">Number {{i + 1}}</v-card-subtitle>

            <v-card-text class="text--primary">
              <div>{{ad.description}}</div>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn :to="'/ad/' + ad.id" class="mr-2">Open</v-btn>
              <app-buy-modal :ad="ad"></app-buy-modal>
            </v-card-actions>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
  <div v-else>
    <v-container>
      <v-layout row>
        <v-flex xs12 class="text-center pt-10">
          <v-progress-circular
            :size="70"
            color="amber"
            indeterminate
          ></v-progress-circular>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
export default {
  computed: {
    promoAds () {
      return this.$store.getters.promoAds
    },
    ads () {
      return this.$store.getters.ads
    },
    loading () {
      return this.$store.getters.loading
    }
  }
}
</script>

<style>
  .ad-link {
    position: absolute;
    bottom: 50px;
    left: 50%;
    background: rgba(0, 0, 0, .5);
    transform: translate(-50%, 0);
    padding: 5px 15px;
    border-radius: 5px;
  }
</style>
