<template src="./CreateArticle.html"></template>

<script>
import axios from "axios";
import Sidebar from "./Sidebar.vue";
import Global from "../Global";
import Article from "../models/Article";
import { required } from "vuelidate/lib/validators";
import swal from "sweetalert";
export default {
  name: "EditArticle",
  components: {
    Sidebar,
  },
  data() {
    return {
      file: "",
      url: Global.url,
      article: new Article("", "", null, ""),
      submitted: false,
      isEdit: true,
    };
  },
  validations: {
    article: {
      title: {
        required,
      },
      content: {
        required,
      },
    },
  },
  mounted() {
    //  console.log(this.article);
    var articleId = this.$route.params.id;
    this.getArticle(articleId);
  },
  methods: {
    fileChange() {
      this.file = this.$refs.file.files[0];
    },
    getArticle(articleId) {
      axios.get(this.url + "article/" + articleId).then((res) => {
        if (res.data.status == "success") {
          this.article = res.data.article;
        }
      });
    },
    save() {
      this.submitted = true;
      var articleId = this.$route.params.id;

      this.$v.$touch();
      if (this.$v.$invalid) {
        return false;
      } else {
        axios
          .put(this.url + "article/" + articleId, this.article)
          .then((res) => {
            if (res.data.status == "success") {
              if (
                this.file != null &&
                this.file != undefined &&
                this.file != ""
              ) {
                const formData = new FormData();
                formData.append("file0", this.file, this.file.name);
                var articleId = res.data.article._id;
                axios
                  .post(this.url + "upload-image/" + articleId, formData)
                  .then((res) => {
                    if (res.data.article) {
                      swal(
                        "Articulo editado correctamente",
                        "Al articulo se ha editado correctamente jajaja",
                        "success"
                      );

                      this.article = res.data.article;
                      this.$router.push("/articulo/" + articleId);
                    } else {
                      //comment
                    }
                  })
                  .catch(() => {
                    swal(
                      "Erro al Crear articulo",
                      "Al articulo no se ha editado jijiji",
                      "error"
                    );
                  });
              } else {
                swal(
                  "Articulo editado correctamente",
                  "Al articulo se ha editado correctamente jajaja",
                  "success"
                );
                this.article = res.data.article;
                this.$router.push("/articulo/" + articleId);
              }
            }
          })
          .catch(() => {
            swal(
              "Erro al Crear articulo",
              "Al articulo no se ha editado jijiji",
              "error"
            );
          });
      }
    },
  },
};
</script>

<style lang="css" scoped>
</style>