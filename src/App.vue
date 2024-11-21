<template>
  <v-app>
    <v-main>
      <CalculaterOperation/>
    </v-main>
  </v-app>
</template>

<script>
import CalculaterOperation from './components/CalculaterOperation.vue';



export default {
  name: 'App',

  components: {
    CalculaterOperation,
  },

  data: () => ({
    //
  }),
}
</script>
