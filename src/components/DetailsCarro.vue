<template>
    <h1>{{ msg }}</h1>
    {{ details }}
</template>

<script>


import axios from 'axios'

export default {
  name: 'Details',
  props: ['details'],

  // created(){
  //   //this.getCarrosById()
  // },

  
  // methods: {
  //     getCarroById () {
  //         axios.get(this.uriBase)
  //           .then(result =>{
  //               this.carro = result.data
  //         })
  //     }
  // }
  
}
</script>