<template>
  <div id="app">
    <img id="logo" src="./assets/book-logo.jpg">
    <router-view/>
     <div class="panel-body">
    <table class="table table-striped">
      <thead>
        <tr>
          <th>Title</th>
          <th>Author</th>
          <th>Cover</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="book in books">
          <td><a v-bind:href="book.url">{{book.title}}</a></td>
          <td>{{book.author}}</td>
          <td><img :src="book.cover" alt="" height="200px"></td>
          <td><span class="glyphicon glyphicon-trash" aria-hidden="true" v-on:click="removeBook(book)"></span></td>
        </tr>
      </tbody>
    </table>
  </div>
  <div class="panel panel-default">
      <div class="panel-heading">
        <h3 class="panel-title">Add New Books</h3>
      </div>
      <div class="panel-body">
         <form id="form" class="form-inline" v-on:submit.prevent="addBook">
          <div class="form-group">
            <label for="bookTitle">Title:</label>
            <input type="text" id="bookTitle" class="form-control" v-model="newBook.title">
          </div>
          <div class="form-group">
            <label for="bookAuthor">Author:</label>
            <input type="text" id="bookAuthor" class="form-control" v-model="newBook.author">
          </div>
          <div class="form-group">
            <label for="bookUrl">Cover Url:</label>
            <input type="text" id="bookUrl" class="form-control" v-model="newBook.cover">
          </div>
          <input type="submit" class="btn btn-primary" value="Add Book">
        </form>
      </div>
    </div>
  </div>

</template>

<script>
  // Initialize Firebase
  import firebase from 'firebase'
  import toastr from 'toastr'
  import configKey from '../configs.js'
  var myKey = configKey.apiKey

  let config = {
    apiKey: myKey,
    authDomain: "booklist-62489.firebaseapp.com",
    databaseURL: "https://booklist-62489.firebaseio.com",
    projectId: "booklist-62489",
    storageBucket: "booklist-62489.appspot.com",
    messagingSenderId: "460391977633"
  };
  let app = firebase.initializeApp(config);
  let db = app.database()

  let booksRef = db.ref('books')

  export default {
    name: 'app',
    firebase: {
      books: booksRef
    },
    data () {
      return {
        newBook: {
          title: '',
          author: '',
          cover: ''
        }
      }
    },
    methods: {
      addBook: function() {
        booksRef.push(this.newBook);
        this.newBook.title = '';
        this.newBook.author = '';
        this.newBook.cover = '';
      },
      removeBook: function(book) {
        booksRef.child(book['.key']).remove()
        toastr.success('Book removed successfully');
      }
    },
  }
</script>
<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
th {
  text-align: center;
}
img#logo {
  width: 300px;
}
</style>
