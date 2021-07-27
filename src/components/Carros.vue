<template>
    <h1>{{ msg }}</h1>
        <div class="col-md-12"> 
            <button class="btn btn-primary">Add Carros</button>
        </div><br>
  <div class="row container-fluid">

    <div class="col-md-12">

      <div class="col-md-8 offset-2">       
          <table class="table">
            <thead>
              <tr>
                <th scope="col">#</th>
                <th scope="col">Nome</th>
                <th scope="col">Modelo</th>
                <th scope="col">Ano Fabricação</th>
                <th scope="col">Ano Modelo</th>
                <th scope="col">Data de Venda</th>
                <th scope="col">Opções</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="carro in carros" :key="carro.id">
                <th scope="row">{{carro.id}}</th>
                <td>{{carro.name}}</td>
                <td>{{carro.anoModel}}</td>
                <td>{{carro.anoFabric}}</td>
                <td>{{carro.anoModel}}</td>
                <td>{{carro.dataVenda}}</td>
                <td>
                  <a @click="details (carro.id)" class="btn btn-outline-warning"><i class="far fa-eye"></i></a>
                  <a @click="datails (carro.id)" class="btn btn-outline-info"><i class="far fa-edit"></i></a>
                </td>
              </tr>

            </tbody>
          </table>
      </div>

    </div>

  </div>

    

</template>

<script>


import axios from 'axios'

export default {
  name: 'Carros',
  props: {
    msg: String
  },

  created(){
    this.getAllCarros()
  },

  data () {
    return {
      uriBase : 'http://127.0.0.1:3000/carros',
      carros: [],

    }

  },
  
  methods: {
      // details (id) {
      //   this.$route.push({
      //     name: 
      //   })
      // },

      getAllCarros () {
          axios.get(this.uriBase)
            .then(result =>{
                this.carros = result.data
          })
      }
  }
  
}
</script>