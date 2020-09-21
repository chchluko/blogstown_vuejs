<template>
    <div class="general">
        <div class="center">
        <section id="content">
                <h2 class="subheader">Pagina</h2>
                
                <h3>{{ id_desde_url }}</h3>
                <button @click="redirigiralblog()">Blog</button>
                <button @click="actualizarnombre()">Actualizar Nombre</button>
                <h4>{{ nombre }}</h4>
            </section>
                                        <Sidebar></Sidebar>
    <div class="clearfix"></div>
  </div>
  </div>
</template>

<script>
import Sidebar from './Sidebar.vue';
export default {

  name: 'Pagina',
      components: {
    Sidebar
  },
  mounted(){
this.id_desde_url = this.$route.params.id;
console.log('componente montado');
  },
  created(){
console.log('componente creado');
  },
  updated(){
console.log('componente actualizado');
  },
  destroyed(){
console.log('componente destruido');
  },
  data () {
    return {
id_desde_url: null,
nombre: 'Jesus Lopez'
    }
  },
  methods:{
      actualizarnombre(){
this.nombre = 'El Oso Rulo'
console.log(this.nombre)
  },
  redirigiralblog(){
        this.$router.push('/blog');
  }
  }
}
</script>

<style lang="css" scoped>
</style>