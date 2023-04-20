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
  height: 30px;
  margin-top: 200px;
  border-radius: 0.5rem;
  border: 1px solid blue;
}

button {
  height: 35px;
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
  height: 30px;
  border-radius: 0.5rem;
  border: 1px solid blue;
}
</style>

<!-- <script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style> -->
