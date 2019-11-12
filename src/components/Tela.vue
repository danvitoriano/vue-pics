<template>
  <div class="corpo">
    <h1 class="centralizado">{{ msg }}</h1>
    <h2>{{ titulo }}</h2>
    <button v-on:click="reverseMessage">Inverter</button>
    <p>{{ message }}</p>
    <input v-model="message" />
    <h3 v-text="titulo + ' kkk'"></h3>
    <span v-if="seen">Mostra isso?</span>
    <h3 v-text="titulo + new Date().toLocaleString()"></h3>
    <img v-bind:src="foto.url" v-bind:alt="foto.alt" />
    <img :src="foto.url" :alt="foto.alt" />
    <ul class="lista-fotos">
      <li v-for="post of posts" v-bind:key="post.id" class="lista-fotos-item">
        <meu-painel :titulo="post.first_name + ' ' + post.last_name">
          <img class="imagem-responsiva" :src="post.avatar" :title="post.email" />
        </meu-painel>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import Painel from './shared/painel/Painel'

export default {
  components: {
    'meu-painel': Painel
  },
  name: "Tela",
  created() {
    axios
      .get("https://reqres.in/api/users")
      .then(response => {
        this.posts = response.data.data;
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
      message: "Olá usuário",
      erros: [],
      posts: [],
      seen: false,
      titulo: "Ola",
      foto: {
        url:
          "https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcTwV4kVzT5McBdGSgqlVeRzubrNH_mOrrkKseDOGFURq20HmsrelEfMU7It",
        alt: "Cachorro"
      },
      fotos: [
        {
          url:
            "https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcTwV4kVzT5McBdGSgqlVeRzubrNH_mOrrkKseDOGFURq20HmsrelEfMU7It",
          alt: "Cachorro",
          i: 1
        },
        {
          url:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTOhmlmzV4-Sifx5BIc2SXeA-1CtZJf8jb8V_vPZyKbXIQJKU-rkxGO6OM",
          alt: "Gato",
          i: 2
        }
      ]
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


</style>
