<template>
  <div>
    <v-form ref="form">
      <v-container grid-list-md fluid>
        <v-layout row wrap>
          <v-flex v-for="i in schema" v-bind="i.columnType">
            <v-text-field
              v-if="i.type == 'text' && !i.hidden"
              v-model="i.model"
              :name="i.name"
              :label="i.label"
              v-validate="{ required: i.required, regex:i.regex}"
            ></v-text-field>

            <v-textarea
              solo
              v-if="i.type == 'text-area' && !i.hidden"
              v-model="i.model"
              :name="i.name"
              :label="i.label"
            ></v-textarea>

            <v-select
              v-if="i.type == 'select' && !i.hidden"
              v-model="i.model"
              :items="i.items"
              :name="i.name"
              :label="i.label"
              v-validate="{ required: i.required, regex:i.regex}"
            ></v-select>

            <v-checkbox
              v-if="i.type == 'checkbox' && !i.hidden "
              v-model="i.model"
              :name="i.name"
              :label="i.label"
            ></v-checkbox>

            <v-radio-group v-model="i.model" row :mandatory="i.required">
              <v-radio v-for="item in i.items" :label="item.label" :value="item.value"></v-radio>
            </v-radio-group>

            <span v-if="i.required">{{ errors.first(`${i.name}`) }}</span>
          </v-flex>
          <v-flex>
            <v-spacer/>
            <v-btn class="submit" color="primary" @click="submit">Submit</v-btn>
          </v-flex>
        </v-layout>
      </v-container>
    </v-form>
  </div>
</template>

<script>
export default {
  props: ["schema"],
  created() {
    console.log(this.schema);
  },
  methods: {
    submit() {
      this.$validator.validateAll().then(result => {
        if (result) {
          console.log(result);
        }
      });
    }
  }
};
</script>

<style>
.submit {
  float: right;
}
</style>