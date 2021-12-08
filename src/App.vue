<template>
  <v-app>
    <v-main>
      <Layout />
    </v-main>
  </v-app>
</template>

<script>
import Layout from './components/Layout'

export default {
  name: 'App',

  components: {
    Layout,
  },

  data: () => ({
    //
  }),
}
</script>
