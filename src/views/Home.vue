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
        <v-subheader class="keyValue">{{value.key}}</v-subheader>
      </v-col>
      <v-col cols="8">
        <v-text-field
            v-model="data[key].value"
            :value="value.value"
            :name="value.key"
            :rules="rules.importKey"
            outlined
        ></v-text-field>
      </v-col>
    </v-row>
    <v-row v-for="(value, key) in newFieldData" v-bind:key="key">
      <v-col cols="4">
        <v-text-field
            v-model="value.key"
            :value="value.key"
            :rules="rules.addedNewKey"
            outlined
            class="keyValue"
        ></v-text-field>
      </v-col>
      <v-col cols="7">
        <v-text-field
            v-model="newFieldData[key].value"
            :value="value.value"
            :name="value.key"
            :rules="rules.addedNewValue"
            outlined
        ></v-text-field>
      </v-col>
      <v-col cols="1">
        <v-btn 
          @click="removeField(index)"
          class="error"
          rounded
        >
          <v-icon dark>
            mdi-trash-can
          </v-icon>
          削除する
        </v-btn>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12" class="pb-0 mt-6">
        <p class="mb-0">
          新規フィールドの作成
        </p>
      </v-col>
      <v-col cols="12">
        <v-divider></v-divider>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="4" class="pb-0">
        <v-text-field
            v-model="newFieldKey"
            label="Key"
            outlined
            :rules="rules.newKey"
        ></v-text-field>
      </v-col>
      <v-col cols="7" class="pb-0">
        <v-text-field
            v-model="newFieldValue"
            label="Value"
            outlined
            :rules="rules.newValue"
        ></v-text-field>
      </v-col>
      <v-col cols="1" class="pt-6">
        <v-btn
            @click="addNewField"
            class="white--text"
            color="black"
            rounded
        >
          <v-icon dark>
            mdi-plus
          </v-icon>
          追加する
        </v-btn>
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
      errorMessage: '',
      newFieldKey: null,
      newFieldValue: null,
      newFieldData: [],
      rules: {
        newKey: [val => (val || '').length > 0 || 'この項目は必須です。'],
        newValue: [val => (val || '').length > 0 || 'この項目は必須です。'],
        addedNewValue: [val => (val || '').length > 0 || 'この項目は必須です。'],
        addedNewKey: [val => (val || '').length > 0 || 'この項目は必須です。'],
        importKey: [val => (val || '').length > 0 || 'この項目は必須です。']
      }
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

      if (this.newFieldData) {
        this.newFieldData.forEach((value, index) => {
          this.data.push({
            key: this.newFieldData[index].key,
            value: this.newFieldData[index].value,
          });
        });
      }

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

      this.newFieldData = [];
      this.newFieldKey = null;
      this.newFieldValue = null;
    },
    addNewField() {

      this.errorHandler = false;

      try {
        this.newFieldData.push({
          key: this.newFieldKey,
          value: this.newFieldValue,
        });
      } catch (e) {
        console.log("Ignore");
        this.errorHandler = true;
      }

      this.newFieldKey = null;
      this.newFieldValue = null;
    },
    removeField (index) {
      this.newFieldData.splice(index, 1)
    }
  }
};
</script>

<style>
.keyValue {
  word-break: break-all;
}
</style>