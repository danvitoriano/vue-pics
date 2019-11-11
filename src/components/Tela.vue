<template>
  <div>
    <h1>{{msg}}</h1>
    <h2>{{titulo}}</h2>
    <h3 v-text="titulo + ' kkk'"></h3>
    <span v-if="seen">Mostra isso?</span>
    <h3 v-text="titulo + new Date().toLocaleString()"></h3>
    <img v-bind:src="foto.url" v-bind:alt="foto.alt">
    <img :src="foto.url" :alt="foto.alt">
    <ul>
      <li v-for="foto of fotos" v-bind:key="foto.i">
        <img :src="foto.url" :alt="foto.alt" />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Tela",
  data() {
    return {
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
</style>
