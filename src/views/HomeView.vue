<template>
<main>
  
        <SearchForm @searchClicked="getData"/>

        <!-- Books -->
        <section id="results">
          <div class="wrapper">
            <h2>Results: {{ totalBooks }}</h2>

          </div>

         

          <div class="wrapper pagination" v-if="paginationRequired">
            <!-- paginate :numberPage :currentPage  -->

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
// import BookCard from "@/components/BookCard.vue"
import Paginator from "@/components/Paginator.vue"
import axios from 'axios'

export default {
  name: 'HomeView',
  components: {
    // HelloWorld
    SearchForm,
    Paginator
    // BookCard,
  },

  data: function(){
    return {
      books: [],
      booksPerPage: 100,
      currentPage: 0,
      totalBooks: 0,
      totalPages: [],
      query: ""

    }
  },

  computed:{
    paginationRequired: function(){
      return (this.totalBooks > this.booksPerPage)
    },
  },  


  methods: {
    setData: function(resp){
      // console.log("sucess: ", resp.docs)
      // this.books = resp.docs

      // // Update pagination info
      // this.query = resp.q
      // this.currentPage = resp.start
      // this.numFound = resp.numFound
      // this.totalPages = Math.ceil(this.numFound / this.itemsPerPage)
    },

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

        console.log(resp)
      })
      .catch(error => {
        console.log(error)
      })

    }

  }
}
</script>
