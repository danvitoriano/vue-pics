<template>
  <div class="corpo">
    <h1 class="centralizado">{{ msg }}</h1>
    <h2>{{ titulo }}</h2>
    <input
      type="search"
      v-on:input="filtro = $event.target.value"
      class="filtro"
      placeholder="filtre pelo título da foto"
    />
    {{filtro}}
    <ul class="lista-fotos">
      <li v-for="foto of fotosComFiltro" v-bind:key="foto.id" class="lista-fotos-item">
        <meu-painel :titulo="foto.first_name">
          <img class="imagem-responsiva" :src="foto.avatar" :title="foto.email" />
        </meu-painel>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import Painel from "./shared/painel/Painel";

export default {
  components: {
    "meu-painel": Painel
  },
  name: "Tela",
  computed: {
    fotosComFiltro() {
      if (this.filtro) {
        // filtra a lista, por enquanto vamos retornar uma lista em branco
        let exp = new RegExp(this.filtro.trim(), "i");
        return this.fotos.filter(foto => exp.test(foto.first_name));
      } else {
        // se o campo estiver vazio, não filtramos, retornamos a lista
        return this.fotos;
      }
    }
  },
  created() {
    axios
      .get("https://reqres.in/api/users")
      .then(response => {
        this.fotos = response.data.data;
      })
      .catch(e => {
        this.erros.push(e);
      });
  },
  methods: {
    reverseMessage() {
      this.titulo = this.titulo
        .split("")
        .reverse()
        .join("");
    }
  },
  data() {
    return {
      filtro: "",
      message: "Olá usuário",
      erros: [],
      fotos: [],
      titulo: "Ola"
    };
  },
  props: {
    msg: String
  }
};
</script>

<style scoped>
.centralizado {
  text-align: center;
}

.corpo {
  font-family: Helvetica, Arial, sans-serif;
  margin: 0 auto;
  width: 96%;
  color: gray;
}

.lista-fotos {
  list-style: none;
}

.lista-fotos .lista-fotos-item {
  display: inline-block;
}

.filtro {
  display: block;
  width: 100%;
}
</style>
