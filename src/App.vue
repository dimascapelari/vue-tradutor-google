<template>
  <div class="container">
    <div>
      <h2 class="titulo">Testando o google tradutor</h2>
    </div>
    <div class="sistema">
      <label>Digite o texto</label>
      <input
        v-model="textoParaTraduzir"
        placeholder="Digite o texto em Português..."
      />
      <button class="btn" @click="traduzir">TRADUZIR</button>
      <label>Resultado em Inglês</label>
      <textarea v-model="textoTraduzido" disabled></textarea>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import he from "he";

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

      // this.textoTraduzido = resposta.data.data.translations[0].translatedText;
      this.textoTraduzido = he.decode(
        resposta.data.data.translations[0].translatedText
      );
    },
  },
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  align-items: center;
  display: flex;
  flex-direction: column;
  height: 100vh;
  justify-content: center;
}

.titulo {
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  margin-bottom: 80px;
}

.sistema {
  display: flex;
  flex-direction: column;
}

.sistema label {
  text-align: start;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  margin-bottom: 5px;
}

input {
  height: 50px;
  width: 300px;
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
