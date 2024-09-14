<script>
import dungeon from './assets/maps/ICC - ICC-Clan-Hall-Dungeon.png'
import basement from './assets/maps/ICC - ICC-Clan-Hall-Basement.png'
import crafting from './assets/maps/ICC - ICC-Clan-Hall-Crafting-Area.png'
import ground from './assets/maps/ICC - ICC-Clan-Hall-Ground.png'
import first from './assets/maps/ICC - ICC-Clan-Hall-First.png'

export default {
  data() {
    return {
      images: [dungeon, basement, crafting, ground, first],
      slide: 0,
      ticks: ['a', 'b', 'c', 'd', 'e'],
      topImage: '',
      bottomImage: '',
      opacity: 0
    }
  },
  methods: {
    selectMap(index) {
      this.slide = 400 - index
    },
    getIndex(index) {
      return Math.floor(index / 100)
    }
  },
  created() {
    this.topImage = this.images[this.getIndex(this.slide) + 1]
    this.bottomImage = this.images[this.getIndex(this.slide)]
  },
  watch: {
    slide() {
      this.topImage = this.images[this.getIndex(this.slide) + 1]
      this.bottomImage = this.images[this.getIndex(this.slide)]

      this.opacity = (this.slide % 100) / 100
    }
  }
}
</script>

<template>
  <header></header>

  <main>
    <v-container fluid class="pa-0 ma-0 fill-height d-flex">
      <v-row no-gutters class="fill-height">
        <v-col cols="2" class="pa-0 ma-0">
          <v-slider
            v-model="slide"
            direction="vertical"
            min="0"
            max="400"
            step="1"
            show-ticks="always"
            tick-size="0"
            hide-details="false"
            class="my-16"
          >
            <template v-slot:tick-label="{ index }">
              <v-container v-if="index % 100 === 0" class="arrow-card pa-0">
                <v-card
                  width="10vw"
                  height="10vh"
                  :image="images[(400 - index) / 100]"
                  @click="selectMap(index)"
                ></v-card>
              </v-container>
            </template>
          </v-slider>
        </v-col>
        <v-col cols="10" class="pa-0 ma-0">
          <v-container fluid class="pa-0 ma-0 fill-height">
            <div class="outer-div">
              <v-img
                absolute
                :src="topImage"
                height="100vh"
                width="100vw"
                :style="{ opacity: opacity }"
              ></v-img>
              <v-img
                absolute
                :src="bottomImage"
                height="100vh"
                width="100vw"
                :style="{ opacity: 1 - opacity }"
              ></v-img>
            </div>
          </v-container>
        </v-col>
      </v-row>
    </v-container>
  </main>
</template>

<style>
.v-input__control {
  height: calc(100vh - 132px);
}

.slider-margin {
  margin-left: 5vw;
}

.arrow-card::before {
  border-right: 6px solid currentColor;
  border-top: 6px solid transparent;
  border-left: 6px solid transparent;
  border-bottom: 6px solid transparent;
  top: 4.5vh;
  left: -12px;
  content: '';
  width: 0;
  height: 0;
  position: absolute;
}

.outer-div {
  position: relative;
  width: 100%;
  height: 100%;
}
</style>
