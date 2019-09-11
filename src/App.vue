<template>
  <v-app id="app">
    <navigation />
    <componentas />
   
    <v-content>
      
        <router-view></router-view>
     
    </v-content>
 
  </v-app>
</template>

<script>

  import navigation from './components/navigation';
  import componentas from './components/componentas.vue';

  export default {
    components: {
    navigation,
    componentas
  },
    name: 'App',
    props: {
      source: String,
    },
    data: () => ({
      drawer: null,
    }),
  }
</script>

<style lang="scss">
//Strange, cause here it works! 
main {
 background-image: url('./assets/medis.jpg');
 background-size: cover;
}
  
</style>