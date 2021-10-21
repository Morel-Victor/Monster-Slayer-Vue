<template>
  <v-app>
    <v-main>
      <v-app-bar dark hide-on-scroll fade-img-on-scroll>
        <v-spacer></v-spacer>
        <v-img
          src=".\assets\HydreGauche.png"
          max-height="50px"
          max-width="50px"
        >
        </v-img>
        <div class="pt-2 title-font">Monster Slayer</div>
        <v-img
          src=".\assets\HydreDroite.png"
          max-height="50px"
          max-width="50px"
        >
        </v-img>
        <v-spacer></v-spacer>
      </v-app-bar>

      <v-img src=".\assets\backgroundfull.gif">
        <v-container fluid>
          <v-row justify="space-between">
            <v-col cols="12" sm="4" md="3">
              <v-card
                rounded="lg"
                elevation="16"
                hover
                height="100%"
                class="pa-md-3 ml-3"
              >
                <v-img
                  src="https://i.pinimg.com/originals/c4/dd/5d/c4dd5d671bb86d8551e9697c2d9ece06.gif"
                  contain
                >
                </v-img>
                <v-card-title>Player</v-card-title>
                <v-card-text>
                  <v-progress-linear
                    :value="playerHealth"
                    :height="$vuetify.breakpoint.smAndDown ? 10 : 25"
                    color="green"
                  ></v-progress-linear>
                </v-card-text>
                <v-card-title>Mana</v-card-title>
                <v-card-text>
                  <v-progress-linear
                    v-model="playerMana"
                    :height="$vuetify.breakpoint.smAndDown ? 5 : 13"
                    color="blue"
                  ></v-progress-linear>
                </v-card-text>
              </v-card>
            </v-col>

            <v-col cols="12" sm="4" md="6"  class="py-0" align-self="top">
              <v-row>
                <v-col cols="12" md="4">
                  <v-card rounded="lg" elevation="12">
                    <v-card-title class="justify-center counter-font">
                      Win : {{ winCounter }}
                    </v-card-title>
                  </v-card>
                </v-col>
                <v-col cols="12" md="4">
                  <v-card rounded="lg" elevation="12">
                    <v-card-title class="justify-center counter-font">
                      Round : {{ currentRound }}
                    </v-card-title>
                  </v-card>
                </v-col>
                <v-col cols="12" md="4">
                  <v-card rounded="lg" elevation="12">
                    <v-card-title class="justify-center counter-font">
                      Losse : {{ losseCounter }}
                    </v-card-title>
                  </v-card>
                </v-col>
              </v-row>
            </v-col>

            <v-col cols="12" sm="4" md="3">
              <v-card
                class="d flex align-center pa-md-3 mr-3 mx-lg"
                rounded="lg"
                elevation="16"
                hover
                height="100%"
              >
                <v-img
                  src="https://thumbs.gfycat.com/SecretCreamyDairycow-small.gif"
                  contain
                >
                </v-img>
                <v-card-title>Monster</v-card-title>
                <v-card-text>
                  <v-progress-linear
                    v-model="monsterHealth"
                    :height="$vuetify.breakpoint.smAndDown ? 10 : 25"
                    color="red"
                  ></v-progress-linear>
                </v-card-text>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
      </v-img>

      <v-container fluid>
        <v-row>
          <v-col cols="12">
            <v-footer fixed height="50" elevation="8"> </v-footer>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
// function getRandomValue(min, max) {
//   return Math.floor(Math.random() * (max - min)) + min;
// }

export default {
  data() {
    return {
      monsterHealth: 100,
      playerHealth: 100,
      playerMana: 100,
      currentRound: 0,
      winCounter: 0,
      losseCounter: 0,
    };
  },
  computed: {
    monsterBarStyles() {
      if (this.monsterHealth < 0) {
        return { width: "0%" };
      }
      return { width: this.monsterHealth + "%" };
    },
    playeurBarStyles() {
      if (this.playerHealth < 0) {
        return { width: "0%" };
      }
      return { width: this.playerHealth + "%" };
    },
    manaBarStyles() {
      if (this.playerMana < 0) {
        return { width: "0%" };
      }
      return { width: this.playerMana + "%" };
    },
    // specialAttackReady() {
    //   return this.currentRound % 3 !== 0;
    // },
    lowMana() {
      return this.playerMana <= 0;
    },
  },
  watch: {},
  methods: {},
};
</script>

<style>
.title-font {
  font-family: "Bebas Neue";
  font-size: 45px;
}

.counter-font {
  font-family: "New Rocker";
}

.background {
  opacity: 30%;
}

@import url("https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap");
@import url("https://fonts.googleapis.com/css2?family=New+Rocker&display=swap");

</style>
