<template>
    <v-navigation-drawer
    v-model="drawerValue"
    app
    color="#000000"
    mini-variant
    mini-variant-width="110"
  >
    <router-link to="/">
        <v-avatar class="d-block text-center mx-auto mt-4 mb-10" size="80">
      <v-btn class="ma-2" outlined large fab color="white" >
        <v-icon x-large>mdi-home</v-icon>
      </v-btn>
    </v-avatar>
    </router-link>
      <v-card flat color="#151515" class="rounded-xl mx-4 py-10">
        <v-list flat class="" dark>
          <v-list-item-group v-model="selectedItem">
            <v-list-item
              v-for="(item, i) in items"
              :key="i"
              active-class="border"
            >
              <v-list-item-content>
                <v-icon
                  v-text="item.icon"  
                  :color="selectedItem === i ? 'white' : 'grey lighten-1'"
                ></v-icon>
              </v-list-item-content>
            </v-list-item>
          </v-list-item-group>
        </v-list>
      </v-card>
    </v-navigation-drawer>
  </template>
  
  <script>
  export default {
    data() {
      return {
        selectedItem: 0,
        items: [
          { icon: "mdi mdi-format-list-bulleted" },
          { icon: "mdi mdi-plus" },

        ],
      };
    },
    props: ["drawer"],
    computed: {
      drawerComputed: {
        get() {
          return this.drawer;
        },
        set(value) {
          this.$emit("update:drawer", value);
        },
      },
    },
    watch: {
      drawer(newValue) {
        this.drawerValue = newValue;
      },
      drawerValue(newValue) {
        this.drawerComputed = newValue;
      },
    },
  };
  </script>
  
  <style>
  .border {
    margin: 0px 8px;
    background: #6f0dff;
    border-radius: 15px;
    text-decoration: none;
    width: 60px;
    height: 60px;
  }
  .v-list-item-group .v-list-item--active {
    color: white !important;
  }
  .v-list-item__content {
    padding: 20px 0 !important;
  }
  .image {
    border: 1px solid white;
  }
  </style>
  