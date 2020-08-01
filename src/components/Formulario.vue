<template>
  <div>
    <div class="form-container">
      <div>
        <CorFormulario
          @corInputUpdate="corInputUpdate"
          @corLabelUpdate="corLabelUpdate"
          @borderInputUpdate="borderInputUpdate"
          @corButtonUpdate="corButtonUpdate"
          @borderButtonUpdate="borderButtonUpdate"
          @padraoUpdate="padraoUpdate"
          :corInput="corInput"
          :corLabel="corLabel"
          :borderInput="borderInput"
          :corButton="corButton"
          :borderButton="borderButton"
          :padraoReset="padraoReset"
        />
      </div>

      <div class="div-principal" :style="{background: pegaFoto}">
        <button
          class="btn-carregar"
          :style="{color:corButton,borderColor: borderButton }"
          @click="fotosURL"
        >Carregar Foto</button>

        <form class="form-principal" v-for="form in formulario" :key="form.id">
          <label
            :name="form.label"
            :style="{color: corLabel}"
          >{{form.label.replace(/^.{1}/g, form.label[0].toUpperCase())}}</label>
          <input
            :type="form.type"
            :id="form.id"
            v-model="form.input"
            :placeholder="form.placeholder.replace(/^.{1}/g, form.placeholder[0].toUpperCase())"
            :style="{color:corInput, borderColor:borderInput }"
          />
        </form>
        <textarea
          :style="{color:corInput, borderColor: borderInput}"
          placeholder="Descrição"
          v-model="textArea.text"
        ></textarea>
        <button
          class="btn-enviar"
          @click="mostrarInformacao"
          type="submit"
          :style="{color:corButton,borderColor: borderButton }"
        >Enviar</button>
      </div>
    </div>
    <ul>
      <li v-for="info in informacao" :key="info.id">{{info.label}}: {{info.input}}</li>
      <li>
        <p>
          {{pegarTextArea.descricao}}:
          {{pegarTextArea.text}}
        </p>
      </li>
    </ul>
  </div>
</template>

<script>
import CorFormulario from "@/components/CorFormulario.vue";
export default {
  name: "Formulario",
  components: {
    CorFormulario,
  },
  data() {
    return {
      corLabel: "#000000",
      corInput: "#000000",
      borderInput: "#e0e0e0",
      corButton: "#000000",
      borderButton: "#e0e0e0",
      padraoReset: "",
      informacao: "",
      pegaFoto: {},
      textArea: {
        text: "",
        descricao: "Descriçao",
      },
      pegarTextArea: "",
      formulario: {
        formNome: {
          label: "Nome",
          input: "",
          placeholder: "nome",
          type: "text",
          id: "nome",
        },
        formEmail: {
          label: "Email",
          input: "",
          placeholder: "email",
          type: "email",
          id: "email",
        },

        formTelefone: {
          label: "Telefone",
          input: "",
          placeholder: "(XX) 0000-0000",
          type: "phone",
          id: "phone",
        },
      },
    };
  },
  methods: {
    corLabelUpdate(corLabel) {
      this.corLabel = corLabel;
    },
    corInputUpdate(corInput) {
      this.corInput = corInput;
    },

    borderInputUpdate(borderInput) {
      this.borderInput = borderInput;
    },
    corButtonUpdate(corButton) {
      this.corButton = corButton;
    },
    borderButtonUpdate(borderButton) {
      this.borderButton = borderButton;
    },
    padraoUpdate(padraoReset) {
      this.padraoReset = padraoReset;
      this.pegaFoto = "none";
    },
    mostrarInformacao() {
      if (
        this.formulario.formNome.input != "" &&
        this.formulario.formEmail.input != "" &&
        this.formulario.formTelefone.input != "" &&
        this.textArea.text != ""
      ) {
        this.informacao = this.formulario;
        this.pegarTextArea = this.textArea;
      }
    },
    async fotosURL() {
      try {
        const url = await fetch("https://dog.ceo/api/breeds/image/random");
        this.pegaFoto = await url.json();

        this.pegaFoto = `url(${this.pegaFoto.message})no-repeat center/cover `;
      } catch (erro) {
        console.log(Error(erro));
      }
    },
  },
};
</script>

<style scoped>
.form-container {
  display: flex;
  max-width: 960px;
  justify-content: space-between;
  margin-top: 20px;
  margin-bottom: 40px;
}
@media screen and (max-width: 740px) {
  .form-container {
    display: block;
    margin-top: 0px;
    margin-bottom: 40px;
  }
}

.div-principal {
  flex: 1;
  max-width: 500px;
  font-size: 1rem;
  margin: 0 auto;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  padding: 40px 30px;
}

@media screen and (max-width: 740px) {
  .div-principal {
    max-width: 90%;
  }
}

.form-principal label {
  margin-bottom: 10px;
}

.form-principal input {
  background: none;
  border: none;
  margin-bottom: 30px;
  font-size: 1rem;
  width: 100%;
  border-bottom: 1px solid #e0e0e0;
  outline: none;
  z-index: 2;
}
.form-principal input:focus,
.form-principal input:hover {
  border-bottom: 2px solid #b2b2b2;
}
textarea {
  width: 80%;
  height: 150px;
  margin-bottom: 10px;
  outline: none;
  border: 1px solid #e0e0e0;
  background: none;
}
textarea:focus,
textarea:hover {
  border: 2px solid #b2b2b2;
}
button {
  display: block;
  background: none;
  text-transform: uppercase;
  padding: 10px 20px;
  cursor: pointer;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
  outline: none;
}
button:hover {
  transform: scale(1.1);
}
button:focus {
  border-color: #b2b2b2;
}
.btn-carregar {
  margin: 0 auto;
  margin-bottom: 40px;
}

ul {
  max-width: 960px;
  margin: 0 auto;
  margin-top: 40px;
}
ul li {
  margin-bottom: 20px;
  padding-left: 60px;
  max-width: 700px;
  font-size: 1rem;
}

@media screen and (max-width: 740px) {
  ul li {
    padding-left: 0px;
  }
}
</style>