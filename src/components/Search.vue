<template>
  <div class="general">
    <Slider :titulo="'Busqueda: ' + searchString"></Slider>
    <div class="center">
      <section id="content">
        <h1 class="subheader" v-if="articles">Articulos encontrados</h1>
        <h1 class="subheader" v-else>Sin resultados</h1>
        <!--Listado articulos-->
        <div id="articles" v-if="articles">
          <Articles :articles="articles"></Articles>
        </div>
        <div v-else>
          <h2>No hay articulos para mostrar</h2>
        </div>
      </section>
      <Sidebar></Sidebar>
      <div class="clearfix"></div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Slider from "./Slider.vue";
import Sidebar from "./Sidebar.vue";
import Global from "../Global";
import Articles from "./Articles.vue";

export default {
  name: "Search",
  components: {
    Sidebar,
    Slider,
    Articles
  },
  mounted() {
    this.searchString = this.$route.params.searchString;
    this.getArticlesBySearch(this.searchString);
  },
  methods: {
    getArticlesBySearch(searchString) {
      axios.get(this.url + "search/" + searchString).then((res) => {
        if (res.data.status == "success") {
          this.articles = res.data.articles;
         // console.log(this.articles);
        }
      });
    },
  },
  data() {
    return { url: Global.url, articles: [] , searchString: null};
  },
};
</script>

<style lang="css" scoped>
</style>