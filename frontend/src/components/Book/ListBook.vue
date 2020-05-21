<template lang="html">
  <div class="container rounded bg-success py-2">
    <div class="container rounded">
      <div class="row">
        <div class="col text-left">

          <div class="">
            <h2 class="text-center"><font color="#000000" size="10" face="Comic Sans MS, Arial, MS Sans Serif">
              Libreria
            </font></h2>
            <b-button size="sm" :to="{name: 'NewBook'}" variant="primary">
              Nuevo libro
            </b-button>
          </div>
          <br>
          <div class="col-md-12">
            <b-table striped hover :items="books" :fields="fields">
              <template v-slot:cell(action)="data">
                <b-button size="sm" variant="primary" :to="{ name:'EditBook', params: {bookId: data.item.id} }">
                  Editar
                </b-button>
                <b-button size="sm" variant="danger" :to="{ name:'DeleteBook', params: {bookId: data.item.id} }">
                  Eliminar
                </b-button>
              </template>
            </b-table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default{
  data(){
    return{
      fields: [
        {key: 'title', label: 'Título'},
        {key: 'description', label: 'Descripción'},
        {key: 'action', label: ''}
      ],
      books: []
    }
  },
  methods: {
    getBooks(){
      const path = 'http://localhost:8000/rest/books/'
      axios.get(path).then((response) => {
        this.books = response.data
      })
      .catch((error) => {
        console.log(error)
      })
    }
  },
  created(){
    this.getBooks()
  }
}
</script>

<style lang="css" scoped>
</style>
