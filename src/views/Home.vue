<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <h2>Upload JSON File</h2>
      </v-col>
      <v-col cols="12">
          <v-divider></v-divider>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="6">
        <!-- <input type="file" @change="loadTextFromFile" /> -->
        <v-file-input
          id="selectFiles"
          label="File input"
          outlined
          dense
          prepend-icon="mdi-paperclip"
          @change="loadTextFromFile"
        ></v-file-input>
      </v-col>
      <v-col cols="6">
        <v-btn
          id="import"
          class="white--text"
          color="black"
          rounded
        >
          Submit
        </v-btn>
      </v-col>
      <v-col cols="6">
        <pre id="result"></pre>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <h2>Update JSON File</h2>
      </v-col>
      <v-col cols="12">
          <v-divider></v-divider>
      </v-col>
    </v-row>
    <v-row v-for="(value, key, index) in users" v-bind:key="index">
        <v-col cols="4">
          <v-subheader>{{key}}</v-subheader>
        </v-col>
        <v-col cols="8">
          <!-- <input :type="text" :name="key" :v-model="test" :value="value" /> -->
          <v-text-field
            :v-model="uploadFile"
            :value="value"
            :name="key"
            outlined
          ></v-text-field>
        </v-col>
        <!-- <input :v-model="value" type="text" :value="value"/> -->
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      uploadFile: null,
      users: [],
      result: null,
      selectFiles: null,
      value: null,
    };
  },
  methods:{
    loadTextFromFile() {
      const file = document.getElementById('selectFiles').files[0];
      // const file = ev.target.files[0];
      const reader = new FileReader();

      reader.onload = e => {
        this.users = JSON.parse(e.target.result);

      }
      reader.readAsText(file);

    },
  }
};
</script>