<template>
    <article class="article-item">
                        <div class="image-wrap">
                            <img 
                            :src="pelicula.image" 
                            :alt="pelicula.title" 
                            />
                        </div>
    
                        <h2>{{ pelicula.title }}</h2>
                        <span class="date" :class="{
                              yeargreen:pelicula.year >=2005,
                              yearred:pelicula.year <2005
                    }">
                            {{ pelicula.year }}
                        </span>
                        <a href="#">Leer más</a>
<input type="button" value="Marcar como favorita" @click="pasarFavtoF(pelicula)" />
                        <div class="clearfix"></div>
                    </article>
</template>

<script>
export default {

  name: 'Pelicula',
  props: ['pelicula'],
  methods:{
    pasarFavtoF(pelicula){
      //console.log(pelicula);
     // alert("boton pulsado");
      this.$emit('favorita',pelicula); //se emite el evento
    }
  },
  data () {
    return {

    }
  }
}
</script>

<style lang="css" scoped>
</style>