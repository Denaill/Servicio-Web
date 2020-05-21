<template lang="html">
  <div class="container">
    <div class="row">
      <div class="col text-left">
        <h2>Editar Libro</h2>
      </div>
    </div>
    <div class="row">
      <div class="col">
        <div class="card">
          <div class="card-body">
            <form @submit="onSubmit">
              <div class="form-group row">
                <label for="title" class="col-sm-2 col-form-label">Título</label>
                <div class="col-sm-6">
                  <input type="text" placeholder="Título" name="title" class="form-control" v-model.trim="form.title"></input>
                </div>
              </div>

              <div class="form-group row">
                <label for="description" class="col-sm-2 col-form-label">Descripción</label>
                <div class="col-sm-6">
                  <textarea name="description" class="form-control" placeholder="Descripción" rows="3" v-model.trim="form.description"></textarea>
                </div>
              </div>

              <div class="rows">
                <div class="col text-left">
                  <b-button type="submit" variant="primary">Editar</b-button>
                  <b-button type="submit" class="btn-large-space" :to="{ name: 'ListBook' }">Cancelar</b-button>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
  </div>
</div>
</template>

<script>
import axios from 'axios'
import swal from 'sweetalert'

export default{
  data() {
    return {
      bookId: this.$route.params.bookId,
      form: {
        title: '',
        description: ''
      }
    }
  },
  methods: {
    onSubmit(evt){
      evt.preventDefault()
      const path = 'http://localhost:8000/rest/books/'+this.bookId+'/'
      axios.put(path, this.form).then((response) => {
        this.form.title = response.data.title
        this.form.description = response.data.description
        swal("Libro actualizado exitosamente!", "", "success")
      })
      .cath((error) => {
        console.log(error)
      })
    },
    getBook(){
      const path = 'http://localhost:8000/rest/books/'+this.bookId+'/'
      axios.get(path).then((response) => {
        this.form.title = response.data.title
        this.form.description = response.data.description
      })
      .cath((error) => {
        console.log(error)
      })
    }
  },
  created(){
    //console.log(this.$route.params.id);
    //this.bookId = this.$route.params.id;
    this.getBook()
  }
}
</script>

<style lang="css" scoped>
</style>
