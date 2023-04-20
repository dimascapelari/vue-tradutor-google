<template>
  <div class="container">
    <input v-model="textoParaTraduzir" />
    <button class="btn" @click="traduzir">TRADUZIR</button>
    <textarea v-model="textoTraduzido"></textarea>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      textoParaTraduzir: "",
      textoTraduzido: "",
      idiomaDestino: "en", // idioma padrão é o inglês
    };
  },
  methods: {
    async traduzir() {
      const url =
        "https://translation.googleapis.com/language/translate/v2?key=AIzaSyBEi1XMCtf7qYjq0y2B4tsWDUTPalhLQ2w";

      const resposta = await axios.post(url, {
        q: this.textoParaTraduzir,
        target: this.idiomaDestino,
      });

      this.textoTraduzido = resposta.data.data.translations[0].translatedText;
    },
  },
};
</script>
<style>
.container {
  align-items: center;
  display: flex;
  flex-direction: column;
}
input {
  height: 50px;
  width: 300px;
  margin-top: 200px;
  border-radius: 0.5rem;
  border: 1px solid blue;
}

button {
  height: 35px;
  width: 150px;
  background-color: blue;
  color: white;
  margin: 30px auto;
  border: none;
  border-radius: 0.5rem;
  border: 1px solid blue;
  cursor: pointer;
}

.container button:active {
  background-color: rgb(55, 95, 170);
}

textarea {
  height: 50px;
  border-radius: 0.5rem;
  border: 1px solid blue;
  width: 300px;
}
</style>
