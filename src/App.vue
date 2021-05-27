<template>
  <v-app>
    <v-app-bar
        app
        color="primary"
        dark>
      <v-spacer></v-spacer>
      <v-icon>mdi-open-in-new</v-icon>
    </v-app-bar>
    <v-main>
      <HelloWorld/>
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',

  components: {
    HelloWorld,
  },

  data: () => ({
    //
  }),
};
</script>
