<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <h2>JSONファイルのインポート</h2>
      </v-col>
      <v-col cols="12">
          <v-divider></v-divider>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="6">
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
    <v-row>
      <v-col cols="12">
        <v-btn
          @click="getNewJSONValue"
          :key="uploadFile"
          class="white--text"
          color="black"
          rounded
        >
          Export
        </v-btn>
        <!-- {{data}} -->
      </v-col>
    </v-row>
    <!-- <div id="element">
      <div v-if="!data.length">Invalid</div> -->
      <v-row v-for="(value, key) in data" v-bind:key="key">
          <v-col cols="4">
            <v-subheader>{{value.key}}</v-subheader>
          </v-col>
          <v-col cols="8">
            <v-text-field
              v-model="data[key].value"
              :value="value.value"
              :name="value.key"
              outlined
            ></v-text-field>
          </v-col>
      </v-row>
    <!-- </div> -->
  </v-container>
</template>

<script>
import downloadjs from 'downloadjs';

export default {
  data() {
    return {
      uploadFile: null,
      data: [],
      result: null,
      selectFiles: null,
      value: null
    };
  },
  methods:{
    loadTextFromFile() {
      
      this.errorMessage = '';
      this.data = [];
      const file = document.getElementById('selectFiles').files[0];
      const reader = new FileReader();

      reader.onload = e => {
          Object.keys(JSON.parse(e.target.result)).forEach(key => {
            this.data.push({
              key: key,
              value: JSON.parse(e.target.result)[key],
            });
          });
      }

      reader.readAsText(file);
    },
    getNewJSONValue() {
      var jsonStr = '{';
      var l = this.data.length;
      var i = 0;
      this.data.forEach((value, index) => {
        i++;
        jsonStr += '"'+this.data[index].key+'":'
            + '"' + this.data[index].value + '"';

        if (l !== i) {
          jsonStr += ',';
        }
      });

      jsonStr += '}';

      downloadjs(jsonStr, "apidata.json", "text/plain");
    }
  }
};
</script>