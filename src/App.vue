<template>

  <v-app>

    <v-app-bar app dark hide-on-scroll elevate-on-scroll class="pa-0">
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

    <v-main>

      <v-container fluid class="pa-0">

          <div id="parallax-container">

            <img src="@/assets/ciel-full.png" alt="ciel">
            <img src="@/assets/lave.gif" alt="eau">
            <img src="@/assets/nuage-full.png" alt="nuage">
            <img src="@/assets/montagne-clair-full.png" alt="montagne clair">
            <img src="@/assets/montagne-noir-full.png" alt="montagne sombre">
            <img src="@/assets/eau-full.png" alt="eau">

            <div v-if="attackAnimation">

              <img src="@/assets/attack2.gif" alt="animation attack">

            </div>

            <v-row>

              <v-col cols="12" sm="4" md="3" class="py-11">

                <v-card
                        rounded="lg"
                        elevation="16"
                        hover
                        height="100%"
                        class="pa-md-5 ml-10"
                    >
                      <v-img
                          src="@/assets/nyancat.gif"
                          contain
                          height=""
                      >
                      </v-img>
                      <v-card-title class="pa-2">Life</v-card-title>
                      <v-card-text class="pr-2 pl-2 pb-1">
                        <v-progress-linear
                            :value="playerHealth"
                            :height="$vuetify.breakpoint.smAndDown ? 10 : 25"
                            color="green"

                        >
                          {{playerHealth}} / 100
                        </v-progress-linear>
                      </v-card-text>
                      <v-card-title class="pa-2">Mana</v-card-title>
                      <v-card-text class="pr-2 pl-2 pb-1">
                        <v-progress-linear
                            v-model="playerMana"
                            :height="$vuetify.breakpoint.smAndDown ? 10 : 18"
                            color="blue darken-2"
                        >
                          {{playerMana}} / 100
                        </v-progress-linear>
                      </v-card-text >
                      <v-card-title class="pa-2">Poison</v-card-title>
                      <v-card-text class="pr-2 pl-2 pb-0">
                        <v-progress-linear
                            v-model="playerPoison"
                            :height="$vuetify.breakpoint.smAndDown ? 10 : 18"
                            color="green darken-2"
                        >
                          {{playerPoison}} / 100
                        </v-progress-linear>
                      </v-card-text>

                    </v-card>

              </v-col>

              <v-col cols="12" sm="4" md="6"  class="py-8">

                <v-row>

                  <v-col cols="12" md="4" >
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
                        Loss : {{ lossCounter }}
                      </v-card-title>
                    </v-card>
                  </v-col>

                </v-row>

                <v-row justify="center">

                  <v-col cols="12" md="8" align-self="center">

                    <div class="text-center">

                      <v-menu
                          offset-y
                          nudge-bottom="15"
                          nudge-left="110"
                          rounded="lg"
                          transition="slide-y-transition"
                          open-on-hover
                      >

                        <template v-slot:activator="{ on, attrs }">
                          <v-btn
                              class="align-center"
                              dark
                              v-bind="attrs"
                              v-on="on"
                          >
                            Show Battle Logs
                          </v-btn>
                        </template>

                        <v-container fluid class="d-flex justify-center">

                          <v-list elevation="24" class="text-center pt-4">
                            <v-list-item
                                v-for="Log in Logs"
                                :key="Log.roundNumber"
                            >
                              <v-list-item-title>{{ Log.roundNumber }}</v-list-item-title>
                            </v-list-item>
                          </v-list>

                          <v-list elevation="24" >
                            <v-list-item
                                v-for="Log in Logs"
                                :key="Log.actionBy"
                            >
                              <v-list-item-title class="text-center pa-4">{{ Log.actionBy }}</v-list-item-title>
                            </v-list-item>
                          </v-list>

                          <v-list elevation="24" >
                            <v-list-item
                                v-for="Log in Logs"
                                :key="Log.typeAttack"
                            >
                              <v-list-item-title class="text-center pa-4">{{ Log.typeAttack }}</v-list-item-title>
                            </v-list-item>
                          </v-list>

                          <v-list elevation="24">
                            <v-list-item
                                v-for="Log in Logs"
                                :key="Log.value"
                            >
                              <v-list-item-title class="text-center pa-4">{{ Log.value }}</v-list-item-title>
                            </v-list-item>
                          </v-list>

                        </v-container>

                      </v-menu>

                    </div>

                  </v-col>

                </v-row>

              </v-col>

              <v-col cols="12" sm="4" md="3" class="py-11">
                <v-card
                    class="d flex align-center pa-md-5 mr-10 mx-lg"
                    rounded="lg"
                    elevation="16"
                    hover
                    height="100%"
                >
                  <v-img
                      src="@/assets/monster.gif"
                      contain
                  >
                  </v-img>

                  <v-card-title class="pa-2">Life</v-card-title>
                  <v-card-text class="pr-2 pl-2 pb-1">
                    <v-progress-linear
                        v-model="monsterHealth"
                        :height="$vuetify.breakpoint.smAndDown ? 10 : 25"

                        color="red darken-2"
                    >
                      {{monsterHealth}} / 100
                    </v-progress-linear>

                  </v-card-text>

                  <v-card-title class="pa-2">Mana</v-card-title>
                  <v-card-text class="pr-2 pl-2 pb-1">
                    <v-progress-linear
                        v-model="monsterMana"
                        :height="$vuetify.breakpoint.smAndDown ? 10 : 18"

                        color="blue darken-2"
                    >
                      {{monsterMana}} / 100
                    </v-progress-linear>
                  </v-card-text>

                  <v-card-title class="pa-2">Poison </v-card-title>
                  <v-card-text class="pr-2 pl-2 pb-0">
                    <v-progress-linear
                        v-model="monsterPoison"
                        :height="$vuetify.breakpoint.smAndDown ? 10 : 18"

                        color="green darken-2"
                    >
                      {{monsterPoison}} / 100
                    </v-progress-linear>
                  </v-card-text>

                </v-card>
              </v-col>

            </v-row>

            <v-container fluid>

              <v-row justify="center">

                <v-col cols="12" md="3" class="pt-3 align-center">

                    <v-btn
                        id="btn-weapons"
                        class="pa-1 "
                        width="365px"
                        height="80px"
                        depressed
                        elevation="24"
                        large
                        block
                        x-large
                        @click="$vuetify.goTo('#return', {duration: 3000, offset: 0})"
                    >
                      <v-img class="" width="65" height="65" src="@/assets/pointy-sword-red-gauche.png" alt="épée sombre">
                      </v-img>
                      <h1 class="pt-2">
                        W E A P O N S
                      </h1>
                      <v-img class="" width="65" height="65" src="@/assets/pointy-sword-red.png" alt="épée sombre">
                      </v-img>

                    </v-btn>

                </v-col>

              </v-row>

            </v-container>

            <v-container fluid>

              <v-row justify="center" class="pa-16">

                <v-col cols="12" md="12" class="pa-16">

                  <v-card class="pa-3 weapons" elevation="24" outlined>

                    <v-card class="weapons2" height="650" elevation="24" outlined>

                      <v-row>

                        <v-col cols="12" md="2">
                          <h1 class="pl-12 pt-8 pb-8">RULES :</h1>
                        </v-col>

                        <v-col class="text-start pt-11" cols="12" md="10">
                          <p id="rules">
                            Attack the monster with weapons and spells to defeat them. Monster repost with the same attacks as you !<br>
                            Some actions are disabled in the beginning and need some thinks to be enabled
                            Good Luck !
                          </p>
                        </v-col>

                      </v-row>

                      <v-divider width="1450" inset>
                      </v-divider>

                      <v-row>

                          <v-col cols="12" md="2" class="py-12 pl-10 ">

                            <attack-button
                              v-for="attack in attacks"
                              :key="attack.id"
                              :name="attack.name"
                            ></attack-button>

                          </v-col>

                          <v-col cols="12" md="1" class="pt-9">

                            <v-row>

                              <v-col cols="12" md="3" class="pl-0 pr-1">
                                <v-img class="mt-3 mb-10" width="45" src="@/assets/pointy-sword.png"></v-img>
                                <v-img class="mb-10" width="45" src="@/assets/mineral-heart.png"></v-img>
                                <v-img class="mb-10" width="45" src="@/assets/unstable-orb.png"></v-img>
                                <v-img class="mb-10" width="45" src="@/assets/flying-flag.png"></v-img>
                                <v-img class="mb-9" width="45" src="@/assets/potion-of-madness.png"></v-img>
                                <v-img class="mb-5" width="45" src="@/assets/perspective-dice-six-faces-four.png"></v-img>
                              </v-col>

                              <v-col cols="12" md="9" class="pr-0">
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    0 - 7
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    12 - 25
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    0 - 7
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    Death
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    20 2R
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    Luck
                                  </v-card-title>
                                </v-card>
                              </v-col>

                            </v-row>

                          </v-col>

                          <v-col cols="12" md="2" class="py-12 pl-10">


                          </v-col>

                          <v-col cols="12" md="1" class="pt-9">

                            <v-row>

                              <v-col cols="12" md="3" class="pl-0 pr-1">
                                <v-img class="mt-3 mb-10" width="45" src="@/assets/pointy-sword.png"></v-img>
                                <v-img class="mb-10" width="45" src="@/assets/mineral-heart.png"></v-img>
                                <v-img class="mb-10" width="45" src="@/assets/unstable-orb.png"></v-img>
                                <v-img class="mb-10" width="45" src="@/assets/flying-flag.png"></v-img>
                                <v-img class="mb-9" width="45" src="@/assets/potion-of-madness.png"></v-img>
                                <v-img class="mb-5" width="45" src="@/assets/perspective-dice-six-faces-four.png"></v-img>
                              </v-col>

                              <v-col cols="12" md="9" class="pr-0">
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    0 - 7
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    12 - 25
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    0 - 7
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    Death
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    20 2R
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    Luck
                                  </v-card-title>
                                </v-card>
                              </v-col>

                            </v-row>

                          </v-col>

                          <v-col cols="12" md="2" class="py-12 pl-10">



                          </v-col>

                          <v-col cols="12" md="1" class="pt-9">

                            <v-row>

                              <v-col cols="12" md="3" class="pl-0 pr-1">
                                <v-img class="mt-3 mb-10" width="45" src="@/assets/pointy-sword.png"></v-img>
                                <v-img class="mb-10" width="45" src="@/assets/mineral-heart.png"></v-img>
                                <v-img class="mb-10" width="45" src="@/assets/unstable-orb.png"></v-img>
                                <v-img class="mb-10" width="45" src="@/assets/flying-flag.png"></v-img>
                                <v-img class="mb-9" width="45" src="@/assets/potion-of-madness.png"></v-img>
                                <v-img class="mb-5" width="45" src="@/assets/perspective-dice-six-faces-four.png"></v-img>
                              </v-col>

                              <v-col cols="12" md="9" class="pr-0">
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    0 - 7
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    12 - 25
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    0 - 7
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    Death
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    20 2R
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    Luck
                                  </v-card-title>
                                </v-card>
                              </v-col>

                            </v-row>

                          </v-col>

                          <v-col cols="12" md="2" class="py-12 pl-10">


                          </v-col>

                          <v-col cols="12" md="1" class="pt-9">

                            <v-row>

                              <v-col cols="12" md="3" class="pl-0 pr-1">
                                <v-img class="mt-3 mb-10" width="45" src="@/assets/pointy-sword.png"></v-img>
                                <v-img class="mb-10" width="45" src="@/assets/mineral-heart.png"></v-img>
                                <v-img class="mb-10" width="45" src="@/assets/unstable-orb.png"></v-img>
                                <v-img class="mb-10" width="45" src="@/assets/flying-flag.png"></v-img>
                                <v-img class="mb-9" width="45" src="@/assets/potion-of-madness.png"></v-img>
                                <v-img class="mb-5" width="45" src="@/assets/perspective-dice-six-faces-four.png"></v-img>
                              </v-col>

                              <v-col cols="12" md="9" class="pr-0">
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    0 - 7
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    12 - 25
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    0 - 7
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    Death
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    20 2R
                                  </v-card-title>
                                </v-card>
                                <v-card class="mb-5" color="grey darken-3" height="50" width="80">
                                  <v-card-title class="pa-2 justify-center">
                                    Luck
                                  </v-card-title>
                                </v-card>
                              </v-col>

                            </v-row>

                          </v-col>

                      </v-row>

                    </v-card>

                  </v-card>

                </v-col>

              </v-row>

            </v-container>

          </div>

      </v-container>

      <v-bottom-navigation id="return">
        <v-btn dark text @click="$vuetify.goTo('#parallax-container',{duration: 950, offset: 0})">
          <v-icon x-large>mdi-chevron-up</v-icon>
        </v-btn>
      </v-bottom-navigation>

    </v-main>

  </v-app>

</template>

<script>

// RANDOM VALUE //

// function getRandomValue(min, max) {
//   return Math.floor(Math.random() * (max - min)) + min;
// }

// PARALLAX BACKGROUND //

window.addEventListener('scroll', () => {
  let parent = document.getElementById('parallax-container');
  let children = parent.getElementsByTagName('img');
  for(let i = 0; i < children.length; i++) {
    children[i].style.transform = 'translateY(-' + (window.pageYOffset * i / children.length) + 'px)';
  }
}
, false)

import attackButton from "@/components/attackButton";

export default {

  data() {
    return {

      attackAnimation: false,

      monsterHealth: 100,
      monsterMana: 100,
      monsterPoison: 0,

      playerName: "",
      playerHealth: 100,
      playerMana: 100,
      playerPoison: 0,

      currentRound: 0,
      winCounter: 0,
      lossCounter: 0,

      attacks: [
        { id:'attack', name: "Attack", damageValue: 7, healValue: 0, manaValue: 0, poisonValue: 0, },
        { id:'heal', name: "Heal", damageValue: 0, healValue: 25, manaValue: -20, poisonValue: 0, },
        { id:'mana', name: "Mana", damageValue: 0, healValue: 0, manaValue: 20, poisonValue: 0, },
        { id:'surrender', name: "Surrender", damageValue: 100, healValue: 0, manaValue: 0, poisonValue: 0, },
        { id:'poison', name: "Poison", damageValue: 0, healValue: 0, manaValue: 20, poisonValue: 0, },
        { id:'luck', name: "Luck", damageValue: 100, healValue: 0, manaValue: 0, poisonValue: 0, },
      ],

      Logs: [
        { roundNumber: 1, actionBy: 'player', typeAttack: 'Heal', value: 15 },
        { actionBy: 'monster', typeAttack: 'Damage', value: 12 },
        { roundNumber: 2, actionBy: 'player', typeAttack: 'Damage', value: 25 },
        { actionBy: 'monster', typeAttack: 'Damage', value: 45 },
        { roundNumber: 3, actionBy: 'player', typeAttack: 'Mana Up', value: 19 },
        { actionBy: 'monster', typeAttack: 'Damage', value: 1 },
        { roundNumber: 4, actionBy: 'player', typeAttack: 'Poison', value: 3 },
        { actionBy: 'monster', typeAttack: 'Damage', value: 2 },
      ],
    };
  },

  computed: {

    monsterBarStyles() {
      if (this.monsterHealth < 0) {
        return { width: "0%" };
      }
      return { width: this.monsterHealth + "%" };
    },
    playerBarStyles() {
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
  methods: {
    attack() {

    },
    gifAttack() {
      this.attackAnimation = true;
      setTimeout(() => this.attackAnimation = false, 1000)
    },
  },
  components: attackButton
};

</script>

<style>

@import url("https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap");
@import url("https://fonts.googleapis.com/css2?family=New+Rocker&display=swap");

#parallax-container {
  display: block;
  height: 1750px;
}

#parallax-container img {
  background-size: cover !important;
  position: fixed;
  top: 0;
  background-position: center !important;
  transform: translateY(0px);
  height: 1096px;
  width: 100%;
}

.title-font {
  font-family: "Bebas Neue";
  font-size: 45px;
}

.counter-font {
  font-family: "New Rocker";
}

#btn-weapons {
  font-family: "New Rocker";
}

.weapons {
  opacity: 95%;
}
.weapons2 {
  opacity: 95%;
}

#rules {
  font-family: "Bebas Neue";
  font-size: 30px;
}


</style>
