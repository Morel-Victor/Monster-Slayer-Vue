<template>
  <div>
    <v-btn @click="$vuetify.goTo('#parallax-container',{duration: 550, offset: 0})"

    >
      {{ name }}
    </v-btn>
  </div>
</template>

<script>



export default {
  props: ['name'],
  data() {
    return {

    }
  },
  methods: {

  }
}
</script>

<style>

</style>