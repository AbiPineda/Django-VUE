<template>
  <div class="container">
    <div class="row">
      <div class="col text-left">
        <h2>Listado de libros</h2>
        <b-button size="sm" :to="{name: 'NewBook'}" variant="primary">Crear Libro</b-button>
        <div class="col-md-12 p-3">
          <b-table striped hover :items="books" :fields="fields">
            <template v-slot:cell(action)="data">
              <b-button
                size="sm"
                variant="primary"
                :to="{ name: 'EditBook', params: { bookId: data.item.id } }"
                >Editar</b-button
              >
              <b-button
                size="sm"
                variant="danger"
                :to="{ name: 'DeleteBook', params: { bookId: data.item.id } }"
                >Eliminar</b-button
              >
            </template>
          </b-table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      fields: [
        { key: "title", label: "Titulo" },
        { key: "description", label: "Descripcion" },
        { key: "action", label: "" }
      ],
      books: []
    };
  },
  methods: {
    getBooks() {
      const path = "http://localhost:8000/api/v1.0/books/";
      axios
        .get(path)
        .then(response => {
          this.books = response.data;
        })
        .catch(err => {
          /* si existe error */
          console.log(err);
        });
    }
  },
  created() {
    this.getBooks();
  }
};
</script>

<style></style>
