<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        
      </div>
    </v-app-bar>

    <v-content>
      <CardTest/>
    </v-content>
  </v-app>
</template>

<script>
import CardTest from './components/CardTest';

export default {
  name: 'App',

  components: {
    CardTest,
  },

  data: () => ({
    //
  }),
};
</script>
