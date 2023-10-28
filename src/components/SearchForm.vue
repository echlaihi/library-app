<template>
  <section id="search">
        <div class="wrapper">

            <form action="" id="search-form">
                    <input type="text" v-model="query">
    
                    <button @click.prevent="search">Search</button>
            </form>
    
        </div>
    </section>

</template>

<script>

    import axios from "axios"

    export default {
        name: "SearchForm",

        data: () => {
            return {
                query: "",
                offset: 0
            }
        },

        methods: {
        
            search: function(){
                  this.$.emit("searchClicked", this.query, this.offset)  
            }, 

            sanitizeQuery: function(){

            }

        }
    }

</script>