<template>
  <div>
    <v-form ref="form">
      <v-container grid-list-md fluid>
        <v-layout row wrap>
          <v-flex v-for="i in schema" v-bind="i.columnType" v-if="!i.hidden">
            <v-text-field
              v-if="i.type == 'text'"
              v-model="i.model"
              :name="i.name"
              :label="i.label"
              v-validate="{ required: i.required, regex:i.regex}"
            ></v-text-field>

            <v-textarea
              solo
              v-if="i.type == 'text-area' "
              v-model="i.model"
              :name="i.name"
              :label="i.label"
            ></v-textarea>

            <v-select
              v-if="i.type == 'select'"
              v-model="i.model"
              :items="i.items"
              :name="i.name"
              :label="i.label"
              v-validate="{ required: i.required, regex:i.regex}"
            ></v-select>

            <v-checkbox
              v-if="i.type == 'checkbox'"
              v-model="i.model"
              :name="i.name"
              :label="i.label"
            ></v-checkbox>

            <v-radio-group v-if="i.type == 'radio-group'" v-model="i.model" row :mandatory="i.required">
              <v-radio v-for="item in i.items" :label="item.label" :value="item.value"></v-radio>
            </v-radio-group>

            <span v-if="i.required">{{ errors.first(`${i.name}`) }}</span>
          </v-flex>

          <v-flex>
            <v-spacer/>
            <slot name="action"></slot>
            <div v-if="!actionSlotExists">
              <v-btn class="btn" @click="submit">Save</v-btn>
              <v-btn class="btn" @click="cancel">Cancel</v-btn>
            </div>
          </v-flex>
        </v-layout>
      </v-container>
    </v-form>
  </div>
</template>

<script>
export default {
  props: ["schema"],
  computed: {
    actionSlotExists() {
      return !!this.$slots['action'] ;
    }
  },
  methods: {
    submit() {
      this.$validator.validateAll().then(result => {
        if (result) {
          this.$emit("submit", this.schema);
        }
      });
    },
    cancel() {
      this.$emit("cancel", "-1");
    }
  }
};
</script>

<style>
.btn {
  float: right;
}
</style>