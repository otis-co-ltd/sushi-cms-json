<template>
  <v-app id="inspire">
    <v-main>
      <v-container>
        <v-fade-transition mode="out-in">
          <router-view></router-view>
        </v-fade-transition>
      </v-container>
    </v-main>
    <!-- <v-footer color="black" app inset padless absolute>
			<v-container class="white--text text-center">
        Copyright © 2020 OTis Inc. All Rights Reserved
			</v-container>       
			<v-spacer></v-spacer>
		</v-footer> -->
  </v-app>
</template>

<script>
  export default {
    data: () => ({ drawer: null }),
  
    mounted() {
     //this.$fcm.initPush();
    }
  }
</script>
