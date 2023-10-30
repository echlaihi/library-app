<template>
<main>
  
        <SearchForm @searchClicked="getData"/>

        <!-- Books -->
        <section id="results">
          <div class="wrapper">
            
            <div class="alert alert-success" v-if="totalBooks">
                  Results "{{ query }}" : {{ totalBooks }}, page {{ currentPage + 1 }}
            </div>

                      <div v-if="error" class="alert alert-danger">{{ errorMessage }}</div>
          </div>

          <div class="wrapper" id="books">
                    <BookCard v-for="(book, index) in books" :key="index" :book="book"/>
          </div>


         

          <div class="wrapper pagination" v-if="paginationRequired">

            <Paginator 

              :query="query" 
              :totalPages="totalPages" 
              :currentPage="currentPage"
              @getPage="getData"
             
             />
          </div>
        </section>

</main>
  
</template>

<script>
// @ is an alias to /src
import SearchForm from "@/components/SearchForm.vue"
import BookCard from "@/components/BookCard.vue"
import Paginator from "@/components/Paginator.vue"
import axios from 'axios'

export default {
  name: 'HomeView',
  components: {
    // HelloWorld
    SearchForm,
    Paginator,
    BookCard,
  },

  data: function(){
    return {
      books: [],
      booksPerPage: 100,
      currentPage: 0,
      totalBooks: 0,
      totalPages: [],
      query: "",
      error: false

    }
  },

  computed:{
    paginationRequired: function(){
      return (this.totalBooks > this.booksPerPage)
    },
  },  


  methods: {

    getData: function(query, offset){
      console.log("getting offest" , offset );
      axios
      .get(`https://openlibrary.org/search.json?q=${query}&offset=${offset}&limit${this.booksPerPage}`)
      .then(resp => {
        this.books       = resp.data.docs
        this.currentPage = resp.data.offset
        this.totalBooks  = resp.data.numFound
        this.query       = resp.data.q
        this.totalPages  = Math.ceil(this.totalBooks / this.booksPerPage)
        this.error = false
        
      })
      .then(function(){
        
          var height = window.innerHeight
          
          window.scrollTo({
          
          top: height,
          behavior: 'smooth' // Optional, adds a smooth scrolling effect
          });

      })
      .catch(error => {
        this.error = true
        this.errorMessage = error.message
      })

    }

  }
}
</script>
