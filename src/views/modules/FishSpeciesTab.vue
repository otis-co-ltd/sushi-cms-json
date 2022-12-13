<template>

    <v-container fluid>
         <v-row>
              <v-col
                   v-for="image,index in images"
                   :key="index"
                   cols="6"
                   md="6"
                   lg="6"
              >
                   <v-img
                   :src="`./src/assets/modules/FishSpecies/${image.image}`"
                   :lazy-src="`./src/assets/modules/FishSpecies/${image.image}`"
                   class="grey lighten-2 img-shot"
                   contain
                   height="300"
                   @click="viewImageDialog(image.image)"
                   >
                        <template v-slot:placeholder>
                             <v-row
                             class="fill-height ma-0"
                             align="center"
                             justify="center"
                             >
                             <v-progress-circular
                             indeterminate
                             color="grey lighten-5"
                             ></v-progress-circular>
                             </v-row>
                        </template>
                   </v-img>
              </v-col>
         </v-row>
         <v-dialog v-model="dialog">
              <v-card>
                   <v-toolbar
                        dark
                        color="primary"
                   >
                        <v-btn
                        icon
                        dark
                        class="ma-5"
                        @click="dialog = false"
                        >
                             Close
                        </v-btn>
                   </v-toolbar>
                
                   <v-img :src="`./src/assets/modules/FishSpecies/${viewImage}`"></v-img>
              </v-card>
         </v-dialog>
    </v-container>
  
</template>

<script>
export default {

    data: () => ({
         viewImage: "",
         dialog: false,
         images: [
              {
                   image: 'fs1.PNG'
              },
              {
                   image: 'fs2.PNG'
              }
         ]
    }),
    created(){

    },  
    methods: {
         viewImageDialog(image){
              this.dialog = true
              this.viewImage = image
         }
    }
}

</script>