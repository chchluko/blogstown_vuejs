<template>
    <div class="general">
        <div class="center">
 <section id="content">
                <h2 class="subheader">Peliculas</h2>

<div class="favorita" v-if="favorita">
  <h2>Tu pelicula favorita es: {{ favorita.title }}</h2>
</div>

                <div id="articles">
<div v-for="pelicula in peliculasMayuscula" v-bind:key="pelicula.title">
    <Pelicula :pelicula="pelicula" 
    @favorita="AddFavorita"></Pelicula>
</div>
                 
                </div>
                
            </section>
                            <Sidebar></Sidebar>
    <div class="clearfix"></div>
  </div>
  </div>
</template>

<script>
import Pelicula from './Pelicula.vue';

import Sidebar from './Sidebar.vue';
export default {
  name: 'Peliculas',
  components:{ Pelicula,Sidebar
  },methods:{
AddFavorita(favorita){
  this.favorita = favorita;
}
  },filters:{ //se usa con el pipe
mayusculas(value){
return value.toUpperCase();
}
  },
  computed:{
peliculasMayuscula(){
  var peliculasMod = this.peliculas;
  for (var i = 0; i < this.peliculas.length; i++) {
    peliculasMod[i].title = peliculasMod[i].title.toUpperCase();
  }
  return peliculasMod;
}
  },
  data(){
    return {
      favorita:null,
peliculas:[
{title:'Batman',
year:2010,
image:"https://i2.wp.com/wipy.tv/wp-content/uploads/2020/08/guionista-aseguro-que-the-batman-sorprendera-al-publico.jpg"},
{title:'Snatch',year:1998,image:"https://cdn.onebauer.media/one/empire-tmdb/films/107/images/w6Ecdh1Erq285jEVVKmjnkFUIdj.jpg?quality=50&width=1800&ratio=16-9&resizeStyle=aspectfill&format=jpg"},
{title:'IA',year:2005,image:"https://i.pinimg.com/564x/74/bd/80/74bd809ca7a1137696d2c0639a05477e.jpg"}]
    }
  }
}
</script>

<style lang="css" scoped>
</style>