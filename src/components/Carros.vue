<template>
    <h1>{{ msg }}</h1>
        <div class="col-md-12"> 
            <button class="btn btn-primary" @click.prevent="novoForm()">Add Carros</button>
        </div><br>

        

        <div class="form" v-if="isOpen"><!-- v-if="isOpen" -->
          <div class="col-md-8 offset-2">
              <form action="" >
                  <div class="row">
                    <div class="col">
                      <div class="form-outline">
                        <input type="text" v-model="carro.id" class="form-control" hidden/>                        
                      </div>
                    
                      <div class="form-outline">
                        <label class="form-label" for="name">Name</label>
                        <input type="text" v-model="carro.name" class="form-control"  />                        
                      </div>
                    </div>
                    <div class="col">
                      
                      <div class="form-outline">
                        <label class="form-label" for="model">Modelo</label>
                        <input type="text" v-model="carro.model" class="form-control" />                        
                      </div>
                    </div>
                  </div>

                  <hr />

                  <div class="row">
                    <div class="col">
                     
                      <div class="form-outline">
                        <label class="form-label" for="anoFabric">Ano De Fabricação</label>
                        <input type="text" v-model="carro.anoFabric" class="form-control" />                        
                      </div>
                    </div>
                    <div class="col">
                     
                      <div class="form-outline">
                        <label class="form-label" for="anoModel">Ano do Modelo</label>                        
                        <input type="text" v-model="carro.anoModel" class="form-control" />
                      </div>
                    </div>
                    <div class="col">
                      
                      <div class="form-outline">
                        <label class="form-label" for="dataVenda">Data de Venda</label>
                        <input type="date" v-model="carro.dataVenda" class="form-control" />                        
                      </div>
                    </div>
                  </div><br>
                    <div class="col offset-5">
                      <!--Submit input -->
                      <div class="form-outline">                        
                        <button class="btn btn-success" @click.prevent="salvar()" type="submit">Salvar</button>                       
                      </div>
                    </div>
              </form>
          </div><br><br>

        </div>
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
                <td>{{carro.model}}</td>
                <td>{{carro.anoFabric}}</td>
                <td>{{carro.anoModel}}</td>
                <td>{{carro.dataVenda}}</td>
                <td>
                  <!-- <a :href="'/datails/'+carro.id">link</a> -->
                  <a @click="formEditar (carro.id,carro.name, carro.model, carro.anoFabric, carro.anoModel, carro.dataVenda)" class="btn btn-outline-warning"><i class="far fa-edit"></i></a>
                  <a @click="delete (carro.id)" class="btn btn-outline-danger"><i class="far fa-trash-alt"></i></a>
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
      uriBase : 'http://127.0.0.1:3000/carros/',
      carros: [],
      isOpen: false,
      operacao: '',
      carro: {
        id: null,
        name: '',
        model: '',
        anoFabric: '',
        anoModel: '',
        dataVenda: ''
      }

    }

  },
  
  methods: {

      getAllCarros () {
          axios.get(this.uriBase)
            .then(result =>{
                this.carros = result.data
          })
      },

      addCarro(){
        let parametros = {
          name:this.carro.name, 
          model: this.carro.model,
          anoFabric: this.carro.anoFabric,
          anoModel: this.carro.anoModel,
          dataVenda: this.carro.dataVenda
        }
        axios.post(this.uriBase, parametros)
        .then(response =>{
          this.getAllCarros()
        });
          this.carro.name =''; 
          this.carro.model ='';
          this.carro.anoFabric ='';
          this.carro.anoModel ='';
          this.carro.dataVenda ='';

      },

      editar() {

        let parametros = {
          id: this.carro.id,
          name:this.carro.name, 
          model: this.carro.model,
          anoFabric: this.carro.anoFabric,
          anoModel: this.carro.anoModel,
          dataVenda: this.carro.dataVenda,
          
        }
        axios.put(this.uriBase+this.carro.id, parametros)
        .then(response=>{
          this.getAllCarros()
        })
      },

      delete(id){
          axios.delete(this.uriBase+id)
          .then(response=>{
            this.getAllCarros()
          })
      },

      salvar() {
         var criar = "criar"
         var editar = "editar" 

        //alert(this.operacao)
        if(this.operacao === criar){
          //alert("criando")
          this.addCarro()
        }
        if(this.operacao === editar){
          //alert("editando")
          this.editar()
          
        }

      },

      novoForm() {
        this.isOpen = true;
        this.operacao = 'criar';
        this.carro.name ='';
        this.carro.model ='';
        this.carro.anoFabric ='';
        this.carro.anoModel ='';
        this.carro.dataVenda ='';
      },

      formEditar (id, nome, model, anoFabric, anoModel, dataVenda){
        this.operacao = 'editar';
        this.carro.id = id;
        this.carro.name = nome; 
        this.carro.model = model;
        this.carro.anoFabric = anoFabric;
        this.carro.anoModel = anoModel;
        this.carro.dataVenda = dataVenda;
        this.isOpen = true;

      }

  }
  
}
</script>