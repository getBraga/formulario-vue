<template>
  <form>
    <label>Cor-Label</label>
    <input name="corLabel" type="color" v-model=" localCorLabel" />

    <label>Cor-Input</label>
    <input name="colorInput" type="color" v-model="localCorInput" />

    <label>Border-Input</label>
    <input name=" borderInput" type="color" v-model="localBorderInput" />

    <label>Cor-Button</label>
    <input name="color" type="color" v-model="localCorButton" />

    <label>Border-Button</label>
    <input name="borderButton" type="color" v-model="localBorderButton" />

    <input class="default" type="submit" @click.prevent="resetarPadrao" value="Default" />
  </form>
</template>

<script>
export default {
  name: "CorFormulario",
  props: {
    corInput: {
      type: String,
      default: "",
    },
    corLabel: {
      type: String,
      default: "",
    },
    borderInput: {
      type: String,
      default: "",
    },
    corButton: {
      type: String,
      default: "",
    },
    borderButton: {
      type: String,
      default: "",
    },
    padrao: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      localCorLabel: "",
      localCorInput: "",
      localBorderInput: "",
      localCorButton: "",
      localBorderButton: "",
      localPadrao: "",
    };
  },
  methods: {
    resetarPadrao(newValue) {
      this.$emit("padraoUpdate", newValue);
      this.localCorLabel = "#000000";
      this.localCorInput = "#000000";
      this.localBorderInput = "#e0e0e0";
      this.localCorButton = "#000000";
      this.localBorderButton = "#e0e0e0";
    },
  },
  watch: {
    localCorLabel(newValue) {
      this.$emit("corLabelUpdate", newValue);
    },
    localCorInput(newValue) {
      this.$emit("corInputUpdate", newValue);
    },
    localBorderInput(newValue) {
      this.$emit("borderInputUpdate", newValue);
    },
    localCorButton(newValue) {
      this.$emit("corButtonUpdate", newValue);
    },
    localBorderButton(newValue) {
      this.$emit("borderButtonUpdate", newValue);
    },
  },

  created() {
    this.localCorInput = this.corInput;
    this.localCorLabel = this.corLabel;
    this.localBorderInput = this.borderInput;
    this.localCorButton = this.corButton;
    this.localBorderButton = this.borderButton;
    this.localPadrao = this.padrao;
  },
};
</script>

<style scoped>
form {
  background: #b2b2b2;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  padding: 40px 20px;
}
@media screen and (max-width: 740px) {
  form {
    width: 100%;
    margin-bottom: 40px;
  }
}
label {
  margin-bottom: 5px;
  color: #fff;
  text-transform: uppercase;
  letter-spacing: 0.1rem;
  font-size: 1rem;
}
input {
  margin-bottom: 15px;
}
input:hover {
  cursor: pointer;
}
.default {
  padding: 5px 10px;
  background: none;
  border: none;
  border-radius: 4px;
  border: 1px solid #fff;
  color: #fff;
  cursor: pointer;
  text-transform: uppercase;
  font-size: 0.875rem;
  outline: none;
}
</style>