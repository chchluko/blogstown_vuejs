<template src="./CreateArticle.html"></template>

<script>
import axios from "axios";
import Sidebar from "./Sidebar.vue";
import Global from "../Global";
import Article from "../models/Article";
import { required } from "vuelidate/lib/validators";
import swal from "sweetalert";
export default {
  name: "CreateArticle",
  components: {
    Sidebar,
  },
  data() {
    return {
      file: "",
      url: Global.url,
      article: new Article("", "", null, ""),
      submitted: false,
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
  },
  methods: {
    fileChange() {
      this.file = this.$refs.file.files[0];
    },
    save() {
      this.submitted = true;
      this.$v.$touch();
      if (this.$v.$invalid) {
        return false;
      } else {
        axios
          .post(this.url + "save", this.article)
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
                        "Articulo Creado",
                        "Al articulo se ha creado correctamente jajaja",
                        "success"
                      );

                      this.article = res.data.article;
                      this.$router.push("/blog");
                    } else {
                      //comment
                    }
                  })
                  .catch(() => {
                    swal(
                      "Erro al Crear articulo",
                      "Al articulo no se ha creado jijiji",
                      "error"
                    );
                  });
              } else {
                swal(
                  "Articulo Creado",
                  "Al articulo se ha creado correctamente jajaja",
                  "success"
                );

                this.article = res.data.article;
                this.$router.push("/blog");
              }
            }
          })
          .catch(() => {
            swal(
              "Erro al Crear articulo",
              "Al articulo no se ha creado jijiji",
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