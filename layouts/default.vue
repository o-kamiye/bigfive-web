<template>
  <v-app>
    <Toolbar />

    <v-content>
      <v-container class="container">
        <nuxt />
      </v-container>
    </v-content>

    <!-- Snackbar -->
    <v-snackbar
      v-model="snackbar.active"
      :color="snackbar.type === 'error' ? 'error' : 'primary'"
      :bottom="true"
    >
      {{snackbar.message}}
    </v-snackbar>

    <Footer />
  </v-app>
</template>

<script>
import Toolbar from '../components/Toolbar'
import Footer from '../components/Footer'
import { mapState } from 'vuex'

export default {
  name: 'App',
  components: {
    Toolbar,
    Footer
  },
  computed: mapState(['snackbar']),
  head: () => ({
      __dangerouslyDisableSanitizers: ['script'],
      script: [
        {
          innerHTML: `{
            "@context": "http://schema.org",
            "@type" : "Organization",
            "name" : "BigFive",
            "url" : "https://bigfive-test.com",
            "logo": "https://bigfive-test.com/icon.png"
          }`,
          type: 'application/ld+json'
        }
      ]
    })
}
</script>

<style>
a {
  text-decoration: none;
}

.container {
  max-width: 900px;
}

::selection {
  background:black;
  color:white;
}

.v-slider__thumb-label, .v-stepper__step__step {
  font-weight: 800;
}
</style>
