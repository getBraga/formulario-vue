<template>
  <div>
    <Formulario />
  </div>
</template>

<script>
import Formulario from "@/components/Formulario.vue";
export default {
  name: "App",
  data() {
    return {
      isActive: false,
      teste: [],
      criar: Formulario.data().formulario,
    };
  },

  components: {
    Formulario,
  },
};
</script>

<style >
@import url("https://fonts.googleapis.com/css2?family=Roboto&display=swap");
body,
form,
input,
label {
  padding: 0px;
  margin: 0px;
  display: block;
  font-family: "Roboto", sans-serif;
}

* {
  box-sizing: border-box;
}
ul {
  list-style: none;
}
</style>
