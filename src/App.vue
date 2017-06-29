<template>
  <div id="app" class="container">
    <h3 class="text-center">Web App with vue js and firebase</h3>

    <div class="panel panel-default">
      <div class="panel-heading">
        <h1 class="text-center">Add a New Book</h1>
      </div>
      <div class="panel-body">
        <form class="form-inline" v-on:submit.prevent="addBook">
          <div class="form-group">
            <label for="bookTitle">Title:</label>
            <input type="text" class="form-control" v-model="newBook.title">
          </div>
          <div class="form-group">
            <label for="bookAuthor">Author</label>
            <input type="text" class="form-control" v-model="newBook.author">
          </div>
          <div class="form-group">
            <label for="bookUrl">Url</label>
            <input type="text" class="form-control" v-model="newBook.url">
          </div>
          <div class="form-group">
            <input type="submit" class="btn btn-primary" value="Add Book">
          </div>
        </form>
      </div>
    </div>

    <div class="panel panel-default">
      <div class="panel-heading">
        <h1 class="text-center">List Books</h1>
      </div>
      <div class="panel-body">
        <table class="table table-stripped">
          <thead>
            <tr><th>Book</th><th>Author</th><th>Url</th></tr>
          </thead>
          <tbody>
            <tr v-for="book in books">
              <td><a v-bind:href="book.url">{{ book.title }}</a></td>
              <td>{{ book.author }}</td>
              <td>{{ book.url }}</td>
              <td><a v-on:click="removeBook(book)"><i class="glyphicon glyphicon-trash"></i></a></td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import firebase from 'firebase'
//initialize firebase

let config = {
  apiKey: "AIzaSyCKio_krAo1vKGLcN6qEih-wru6HHpmdck",
  authDomain: "vueapp-68be1.firebaseapp.com",
  databaseURL: "https://vueapp-68be1.firebaseio.com",
  projectId: "vueapp-68be1",
  storageBucket: "vueapp-68be1.appspot.com",
  messagingSenderId: "183643240884"
};
var app = firebase.initializeApp(config);

let db = app.database();

let booksref = db.ref('books');

export default {
  name: 'app',
  firebase:{
    books: booksref
  },
  data () {
    return {
      newBook:{
        title:'',
        author:'',
        url:'https://'
      }
    }
  },
  methods:{
    addBook(){
      this.$firebaseRefs.books.push(this.newBook)
    }, removeBook(book){
      this.$firebaseRefs.books.child(book['.key']).remove()
    }
  }
}
</script>

<style>

</style>
