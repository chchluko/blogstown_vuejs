<template>
    <div class="general">
        <div class="center">
    <section id="content">
                <h2 class="subheader">{{ subtitulo }}</h2>

<h2>Reactividad</h2>
<input type="text" v-model="nombre" />
{{ nombre }}
<!--pre>{{ $data }}</pre-->

<h2>Directivas condicionales</h2>
<input type="number" v-model="edad">
<strong>{{ edad }}</strong>
<p v-if="edad && edad >= 18 && edad < 65">
 Eres mayor de edad!!
</p>
<p v-else-if="edad && edad >= 65">
 Eres de avanzada edad!!
</p>
<p v-else>
 Eres menor de edad!!
</p>

<h2>Directiva Iterativa</h2>

<ol>
	<li v-for="pelicula in peliculas" :key="pelicula">{{ pelicula }}</li>
</ol>

    </section>
                                <Sidebar></Sidebar>
    <div class="clearfix"></div>
  </div>
  </div>
</template>

<script>
import Sidebar from './Sidebar.vue';
export default {

  name: 'MiComponente',
    components: {
    Sidebar
  },
  data () {
    return {
        subtitulo: 'soy el subtitulo',
        nombre:'',
        edad: 18,
        peliculas: ['Spiderman','Snach','IA']
    }
  }
}
</script>

<style lang="css" scoped>
</style>