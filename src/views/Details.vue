<template>
  <div class="home">
    <Details msg = "Detalhe do Carro"/>
  </div>
  
</template>

<script>
// @ is an alias to /src
import Details from '@/components/DetailsCarro.vue'
export default {
  name: 'Details',
  components: {
    Details
  }
}
</script>