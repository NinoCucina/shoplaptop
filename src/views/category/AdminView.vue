<template>
    <v-app :style="{ background: $vuetify.theme.themes.dark.background }">
      
    <side-bar-admin :drawer="drawer" />

    </v-app>
  </template>
  
  
  <script>
  import SideBarAdmin from '../../components/SideBarAdmin.vue';
  export default {
  components: { SideBarAdmin },
    
};
  </script>
  
  <style>
  
  </style>
  