<template>
  <v-app id="inspire">
    <v-app-bar
      app
      color="black"
      flat
    >
      <v-container class="py-0 fill-height">
        <v-btn
          v-for="link, index in links"
          :key="index"
          text
          :to="link.link"
          color="white"
        >
          {{link.navName }}
        </v-btn>
      </v-container>
    </v-app-bar>

    <v-main>
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
