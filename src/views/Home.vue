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
      <v-col cols="12">
        <v-file-input
          id="selectFiles"
          label="JSONファイルをアップロードする"
          outlined
          dense
          prepend-icon="mdi-paperclip"
          @change="loadTextFromFile"
        ></v-file-input>
        <p class="red--text ml-6 pa-2"> {{errorMessage}} </p>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <h2>JSONファイルの更新と書き出し</h2>
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
          JSONの書き出し
        </v-btn>
      </v-col>
    </v-row>
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
      value: null,
      keyJson: [],
      dataHandler: null,
      errorHandler: null,
      errorMessage: ''
    };
  },
  methods:{
    loadTextFromFile() {
      
      this.errorMessage = '';
      this.data = [];
      this.errorHandler = false;
      this.dataHandler = null;
      const file = document.getElementById('selectFiles').files[0];
      const reader = new FileReader();

      reader.onload = e => {
        try {
          this.dataHandler = JSON.parse(e.target.result);
        } catch (error) {
          this.errorHandler = true;
          this.errorMessage = 'JSONファイルをアップロードしてください。'
        }

        if (!this.errorHandler) {
          Object.keys(JSON.parse(e.target.result)).forEach(key => {
            this.data.push({
              key: key,
              value: JSON.parse(e.target.result)[key],
            });
          });
        }
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

      downloadjs(jsonStr, "sushi-json.json", "text/plain");
    }
  }
};
</script>