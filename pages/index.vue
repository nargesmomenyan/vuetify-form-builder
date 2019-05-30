<template>
  <div>
    <v-form>
      <v-container grid-list-md fluid>
        <v-layout row wrap>
          <v-flex xs6 md6>
            <v-text-field
              label="Label"
              v-model="control.label"
              v-validate="'required'"
              name="Label"
            ></v-text-field>
            <span>{{ errors.first('Label') }}</span>
          </v-flex>
          <v-flex xs6 md6>
            <v-text-field
              label="Model"
              v-model="control.model"
              v-validate="'required'"
              name="Model"
            ></v-text-field>
            <span>{{ errors.first('Model') }}</span>
          </v-flex>
          <v-flex xs6 md6>
            <v-select
              label="Type"
              :items="types"
              v-model="control.type"
              v-validate="'required'"
              name="Type"
            ></v-select>
            <span>{{ errors.first('Type') }}</span>
          </v-flex>
          <v-flex xs6 md6>
            <v-text-field label="Name" v-model="control.name" v-validate="'required'" name="Name"></v-text-field>
            <span>{{ errors.first('Name') }}</span>
          </v-flex>

          <v-flex xs6 md6>
            <v-checkbox label="validation-required" v-model="control.required"></v-checkbox>
          </v-flex>

          <v-flex xs6 md6>
            <v-text-field label="validation-regex" v-model="control.regex"></v-text-field>
          </v-flex>

          <v-flex xs3 md3>
            <v-select label="Column Type" :items="columnTypes" v-model="control.columnType"></v-select>
          </v-flex>
          <v-flex xs3 md3>
            <v-checkbox label="Hidden" v-model="control.hidden"></v-checkbox>
          </v-flex>
          <v-flex xs3 md3>
            <v-checkbox label="Enabled" v-model="control.enabled"></v-checkbox>
          </v-flex>
          <v-flex xs12 md12>
            <v-btn color="primary" @click="add">Add Control</v-btn>
          </v-flex>
        </v-layout>
      </v-container>
    </v-form>

    <v-divider></v-divider>
    <v-card>
      <FormVuetify :schema="schema"/>
    </v-card>
  </div>
</template>

<script>
import FormVuetify from "~/components/FormVuetify";

export default {
  data() {
    return {
      types: [
        "text",
        "text-area",
        "select",
        "checkbox",
        "group-radio",
        "custom"
      ],
      columnTypes: ["col12", "col6", "col4"],
      control: {
        name: "",
        type: "text",
        label: "",
        hidden: false,
        enabled: true,
        model: "",
        columnType: "col12",
        required: true,
        regex: ""
      },
      schema: []
    };
  },
  methods: {
    add() {
      switch (this.control.columnType) {
        case "col4":
          this.control.columnType = { xs4: true, md4: true };
          break;
        case "col6":
          this.control.columnType = { xs6: true, md6: true };
          break;
        case "col12":
        default:
          this.control.columnType = { xs12: true, md12: true };
          break;
      }
      this.schema.push({ ...this.control });

      this.control.label = "";
      this.control.type = "text";
      this.control.model = "";
      this.control.name = "";
      this.control.hidden = false;
      this.control.enabled = true;
      this.control.columnType = "col12";
      this.control.required = true;
      this.control.regex = "";
      console.log(this.schema);
    },
    buildForm() {}
  },
  components: {
    FormVuetify
  }
};
</script>

