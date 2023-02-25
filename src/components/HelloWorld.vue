<template>
  <div class="column is-half is-offset-one-quarter">
    <section>
      <b-field label="Value 1">
        <b-input type="number" v-model="value1"></b-input>
      </b-field>
      <div class="message">{{ validation.firstError("value1") }}</div>
      <b-field label="Value 2">
        <b-input type="number" v-model="value2"></b-input>
      </b-field>
      <div class="message">{{ validation.firstError("value2") }}</div>

      <b-field label="Select Operation">
        <b-dropdown :disabled="buttonDisable" aria-role="list">
          <template #trigger="{ active }">
            <b-button
              :label="operation"
              type="is-primary"
              :icon-right="active ? 'menu-up' : 'menu-down'"
            />
          </template>

          <b-dropdown-item @click="changeOperation('add')" aria-role="listitem"
            >Add</b-dropdown-item
          >
          <b-dropdown-item @click="changeOperation('sub')" aria-role="listitem"
            >Subtract</b-dropdown-item
          >
          <b-dropdown-item
            @click="changeOperation('divide')"
            aria-role="listitem"
            >Divide</b-dropdown-item
          >
          <b-dropdown-item @click="changeOperation('mul')" aria-role="listitem"
            >Multiply</b-dropdown-item
          >
        </b-dropdown>
      </b-field>

      <b-button
        v-if="buttonNoDekai && !buttonDisable"
        @click="calculation()"
        type="is-primary"
        >Calculate</b-button
      >

      <h1 v-if="result" class="title space">Result:{{ result }}</h1>
    </section>
  </div>
</template>

<script>
import { Validator } from "simple-vue-validator";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  validators: {
    value1: function (value) {
      let check = Validator.value(value).required()._messages;
      if (check.length == 0) {
        this.buttonDisable = false;
      } else {
        this.buttonDisable = true;
      }
      return Validator.value(value).required();
    },
    value2: function (value) {
      let check = Validator.value(value).required()._messages;
      if (check.length == 0) {
        this.buttonDisable = false;
      } else {
        this.buttonDisable = true;
      }
      return Validator.value(value).required();
    },
  },
  data() {
    return {
      value1: null,
      value2: null,
      result: null,
      operation: "Select Operaion",
      buttonNoDekai: true,
      buttonDisable: false,
    };
  },

  beforeMount() {
    if (this.operation === "Select Operaion") {
      this.buttonNoDekai = false;
    }
  },
  mounted(){
    let val1 = this.value1
    let val2 = this.value2
    if(val1 && val2){
      this.buttonDisable = false
    }else {
      this.buttonDisable = true
    }

  },
  watch: {
    operation(newValue, oldValue) {
      console.log(oldValue);
      if (newValue === "Select Operaion") {
        this.buttonNoDekai = false;
      } else {
        this.buttonNoDekai = true;
      }
    },
  },

  methods: {
    calculation() {
      this.result = ''
      switch (this.operation) {
        case "Addition":
          this.result += parseInt(this.value1) + parseInt(this.value2);
          break;
        case "Substraction":
          this.result = parseInt(this.value1) - parseInt(this.value2);
          break;
        case "Division":
          this.result = parseInt(this.value1) / parseInt(this.value2);
          break;
        case "Multiply":
          this.result = parseInt(this.value1) * parseInt(this.value2);
          break;
      }
      this.value1 = ''
      this.value2 = ''
      this.validation.reset()

    },
    changeOperation(message) {
      switch (message) {
        case "add":
          this.operation = "Addition";
          break;
        case "sub":
          this.operation = "Substraction";
          break;
        case "divide":
          this.operation = "Division";
          break;
        case "mul":
          this.operation = "Multiply";
          break;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.space {
  padding-top: 20px;
}
.message {
  background-color: RED;
  border-radius: 4px;
  font-size: 1rem;
}
</style>
