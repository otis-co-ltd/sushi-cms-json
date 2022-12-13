<template>
  <v-app id="inspire">
    <v-app-bar
      app
      color="white"
      flat
    >
      <v-container class="py-0 fill-height">
        <v-btn
          v-for="link, index in links"
          :key="index"
          text
          :to="link.link"
        >
          {{link.navName }}
        </v-btn>
      </v-container>
    </v-app-bar>

    <v-main class="grey lighten-3">
      <v-container>

            <v-sheet
              min-height="70vh"
              rounded="lg"
            >
              <router-view></router-view>
            </v-sheet>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ({
      links: [
        {
          navName: 'JSON file', link: '/',
        },
        {
          navName: 'Modules', link: '/modules'
        }
      ],
    }),
  
    mounted() {
     //this.$fcm.initPush();
    }
  }
</script>
