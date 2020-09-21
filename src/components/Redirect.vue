<template><h1>Redirigiendo...</h1>
</template>

<script>
export default {

  name: 'Redirect',
mounted(){
  this.searchString = this.$route.params.searchString;
  this.$router.push('/buscador/'+this.searchString);
},
  data () {
    return {

    }
  }
}
</script>

<style lang="css" scoped>
</style>