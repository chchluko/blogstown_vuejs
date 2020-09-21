<template>
  <div class="general">
    <Slider titulo="BLOG"></Slider>
    <div class="center">
      <section id="content">
        <h1 class="subheader">Blog</h1>
        <!--Listado articulos-->
        <div id="articles" v-if="articles">
          <Articles :articles="articles"></Articles>
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
  name: "Blog",
  components: {
    Sidebar,
    Slider,
    Articles,
  },
  mounted() {
    this.getArticles();
  },
  methods: {
    getArticles() {
      axios.get(this.url + "articles").then((res) => {
        if (res.data.status == "success") {
          this.articles = res.data.articles;
        //  console.log(this.articles);
        }
      });
    },
  },
  data() {
    return { url: Global.url, articles: [] };
  },
};
</script>

<style lang="css" scoped>
</style>