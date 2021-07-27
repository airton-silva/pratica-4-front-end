<template>
    <h1>{{ msg }}</h1>

</template>

<script>


import axios from 'axios'

export default {
  name: 'Details',
  props: {
    msg: String
  },

  created(){
    this.getAllCarros()
  },

  data () {
    return {
      uriBase : 'http://127.0.0.1:3000/carros',
      carro

    }

  },
  
  methods: {
      getCarroById () {
          axios.get(this.uriBase)
            .then(result =>{
                this.carro = result.data
          })
      }
  }
  
}
</script>