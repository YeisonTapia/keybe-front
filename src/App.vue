<template>
  <v-app >
    <v-content >
      <v-container fluid >
        <v-row
          align="center"
          justify="center" >
          <v-col
            cols="12"
            sm="8"
            md="4" >
            <Weather />    
          </v-col>
        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import Weather from './components/Weather';

export default {
  name: 'App',
  components: {
    HelloWorld,
    Weather
  },
};
</script>
