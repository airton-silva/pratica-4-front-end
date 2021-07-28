<template>
    <h1>{{ msg }}</h1>
        <div class="col-md-12"> 
            <button class="btn btn-primary" @click.prevent="novoForm()">Add Carros</button>
        </div><br>
        <div class="col-md-6 offset-3">
          <p v-if="errors.length">
            <b>Por favor, corrija o(s) seguinte(s) erro(s):</b>
            <ul>
              <li v-for="error in errors" :key="error.id" class="alert alert-warning">{{ error }}</li>
            </ul>
          </p>
        </div>
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
      <div class="row col-md-8 alert alert-default offset-2">

        <div class="col alert alert alert-dark">
          <div class="input-group rounded">
            <input type="search" class="form-control rounded" placeholder="Search" aria-label="Search"
              v-model="search" />
            <span class="input-group-text border-0" id="search-addon" >
              <i class="fas fa-search"></i><a href="#" @click="getByModel()">  buscar</a>
            </span>
          </div>
        </div>
        <div class="col alert alert-dark">
          
          <div class="form-group input-group">
            <div class="row">
              <div class="col-md-6">
                <span>Qnt Registro</span>
              </div>
              <div class="col-md 4">
                <select class="form-control form-control-md" v-model="selected" @blur.prevent="getByQty()">
                  <option>2</option>
                  <option>5</option>
                  <option>10</option>
                  
                </select>
              </div>
            </div>

          </div>
        </div>
      </div>

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
                  <a @click.prevent="formEditar (carro.id,carro.name, carro.model, carro.anoFabric, carro.anoModel, carro.dataVenda)" class="btn btn-outline-warning"><i class="far fa-edit"></i></a>
                  <a @click="deleteRegistro(carro.id)" class="btn btn-outline-danger"><i class="far fa-trash-alt"></i></a>
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
      errors: [],
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

      getByModel() {
        if(this.search === " "){
          this.getAllCarros ()
        }
        axios.get(this.uriBase + "/search?model=" + this.search)
          .then((result) =>{
            this.carros = result.data
        })
      },

      getByQty() {
        //alert(this.selected)
        axios.get(this.uriBase + "qty?qty=" + this.selected)
          .then((result) =>{
            this.carros = result.data
        })
      },

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

      deleteRegistro(id){

        if(confirm('Deseja Realmente Excluir esse Veiculo?'))
          axios.delete(this.uriBase+id)
          .then(response=>{
            this.getAllCarros()
            alert("Carro id: "+ id +" excluido com sucesso")
          })
          .catch(error => {
          console.log(error);
        })
        
      },

      salvar() {
         var criar = "criar"
         var editar = "editar" 

        if(this.operacao === criar){
          this.checkValidate()
          this.addCarro()
          this.isOpen = false

        }
        if(this.operacao === editar){
          this.checkValidate()
          this.editar()
          this.isOpen = false
          
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

      },

      checkValidate(e){
        this.errors = [];

            if (!this.carro.name) {
              this.errors.push('O nome é obrigatório.');
            }            
            if (!this.carro.model) {
              this.errors.push('O modelo é obrigatório.');
            }
            if (!this.carro.anoFabric) {
              this.errors.push('O ano de fabricação é obrigatório.');
            }
            if (!this.carro.anoModel) {
              this.errors.push('O ano do modelo é obrigatório.');
            }
            if (!this.carro.dataVenda) {
              this.errors.push('A data de venda é obrigatório.');
            }


            if (!this.errors.length) {
              return true;
            }

            e.preventDefault();
        
      }

  }
  
}
</script>