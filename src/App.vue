<template>
  <v-app id="inspire">
    <v-app-bar
      app
      color="black"
      flat
    >
      <v-container class="py-0 fill-height">
        <v-btn
          v-for="link in links"
          :key="link"
          text
          color="white"
        >
          {{ link }}
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
        'JSON File',
        'Modules',
      ],
    }),
  
    mounted() {
     //this.$fcm.initPush();
    }
  }
</script>
