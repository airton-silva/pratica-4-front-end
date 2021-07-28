<template>
  <div class="home">

    <Carros msg="Bem vindo A pagina de Carros"/>
  
    
  </div>
  <router-view/>
</template>

<script>
// @ is an alias to /src
import Carros from '@/components/Carros.vue'
//import Form from '@/components/Form.vue'

export default {
  name: 'Home',
  components: {
    Carros,
    //Form

  },

}
</script>