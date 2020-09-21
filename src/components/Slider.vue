<template>
            <div id="slider" :class="{ 
            'slider-big': home,
            'slider-small': !home}">
            <h1>{{ titulo }}</h1>
            <router-link to="/blog" class="btn-white" v-if="home">Ir al Blog</router-link>
        </div>
</template>

<script>
export default {

  name: 'Slider',
  props:['titulo','home'],
  data () {
    return {

    }
  }
}
</script>

<style lang="css" scoped>
</style>