<template>


        <!-- <div class="form" v-if="isOpen"> -->
          <div class="col-md-8 offset-2">
              <form action="" class="needs-validation" novalidate>
                <div class="form-group">
                  <label for="cname">Nome:</label>
                  <input type="text" class="form-control" id="cname" v-model="cname" required>
                  <div class="valid-feedback">Valid.</div>
                  <div class="invalid-feedback">Please fill out this field.</div>
                </div>
                <div class="form-group">
                  <label for="cmodel">Modelo</label>
                  <input type="text" class="form-control" id="cmodel"  v-model="model" required>
                  <div class="valid-feedback">Valid.</div>
                  <div class="invalid-feedback">Please fill out this field.</div>
                </div>

                <div class="form-group">
                  <label for="canof">Ano Fabricação:</label>
                  <input type="text" class="form-control" id="canof" v-model="canof" required>
                  <div class="valid-feedback">Valid.</div>
                  <div class="invalid-feedback">Please fill out this field.</div>
                </div>
                <div class="form-group">
                  <label for="canoModel">anoModelo</label>
                  <input type="text" class="form-control" id="canoModel" v-model="canoModel" required>
                  <div class="valid-feedback">Valid.</div>
                  <div class="invalid-feedback">Please fill out this field.</div>
                </div>
                <div class="form-group">
                  <label for="cdataVenda">Data de Venda</label>
                  <input type="text" class="form-control" id="cdataV" v-model="cdataV" required>
                  <div class="valid-feedback">Valid.</div>
                  <div class="invalid-feedback">Please fill out this field.</div>
                </div>

                <button type="submit" class="btn btn-primary">Submit</button>
              </form>
          </div><br>

        <!-- </div> -->
</template>

<script>
export default {

    name: '',
    props: {
        msg: String
    }
  
}
</script>