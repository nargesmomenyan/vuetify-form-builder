<template>
  <div>
    <v-form>
      <v-container grid-list-md fluid>
        <v-layout row wrap>
          <v-flex xs4 md4>
            <v-text-field
              solo
              label="Label"
              v-model="control.label"
              v-validate="'required'"
              name="Label"
            ></v-text-field>
            <span>{{ errors.first('Label') }}</span>
          </v-flex>
          <v-flex xs4 md4>
            <v-text-field
              solo
              label="Model"
              v-model="control.model"
              v-validate="'required'"
              name="Model"
            ></v-text-field>
            <span>{{ errors.first('Model') }}</span>
          </v-flex>
          <v-flex xs4 md4>
            <v-select
              solo
              label="Type"
              :items="types"
              v-model="control.type"
              v-validate="'required'"
              name="Type"
            ></v-select>
            <span>{{ errors.first('Type') }}</span>
          </v-flex>
          <v-flex xs4 md4>
            <v-text-field
              solo
              label="Name"
              v-model="control.name"
              v-validate="'required'"
              name="Name"
            ></v-text-field>
            <span>{{ errors.first('Name') }}</span>
          </v-flex>
          <v-flex xs4>
            <v-text-field solo label="Items-Model" v-model="control.items"></v-text-field>
          </v-flex>

          <v-flex xs4 md4>
            <v-select solo label="Column Type" :items="columnTypes" v-model="control.columnType"></v-select>
          </v-flex>

          <v-flex xs4 md4>
            <v-checkbox solo label="validation-required" v-model="control.required"></v-checkbox>
          </v-flex>

          <v-flex xs4 md4>
            <v-text-field solo label="validation-regex" v-model="control.regex"></v-text-field>
          </v-flex>

          <v-flex xs2 md2>
            <v-checkbox box label="Hidden" v-model="control.hidden"></v-checkbox>
          </v-flex>
          <v-flex xs2 md2>
            <v-checkbox solo label="Enabled" v-model="control.enabled"></v-checkbox>
          </v-flex>
          <v-flex>
            <v-spacer/>
            <v-btn color="primary" style="float:right" @click="add">Add Control</v-btn>
          </v-flex>
        </v-layout>
      </v-container>
    </v-form>

    <v-divider></v-divider>

    <v-card>
      <v-card-title primary-title style="background-color:#ccc">
        <h4>Form</h4>
      </v-card-title>
      <v-card-text>
        <FormVuetify :schema="schema" @submit="formSubmit" @cancel="formCancel">
          <!-- <template slot="action">
            <v-btn class="btn">Save</v-btn>
          </template>-->
        </FormVuetify>
      </v-card-text>
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
        "checksolo",
        "radio-group",
        "custom"
      ],
      columnTypes: ["col12", "col4", "col4"],
      control: {
        name: "",
        type: "text",
        label: "",
        hidden: false,
        enabled: true,
        model: "",
        columnType: "col12",
        required: true,
        regex: "",
        items: ""
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
        case "col4":
          this.control.columnType = { xs4: true, md4: true };
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
      this.control.items = "";
      console.log(this.schema);
    },
    formSubmit($event) {
      console.log($event);
    },
    formCancel($event) {
      console.log($event);
    }
  },
  components: {
    FormVuetify
  }
};
</script>
<style>
.btn {
  float: right;
}
</style>

