<template>
    <ul id="pagination-bar">

        <li 
        :class="disableIfFirst()"
        @click="getPreviousPage()"
        >&laquo;</li>

        <li 
        v-for="(page, index) in Pages"
         :key="(page, index)" 
         :class="activeIfCurrent(page)"
         @click="getPage(page)"

         >
         {{ index + 1 }}
        </li>

        <li
        :class="disableIfLast()"
        @click="getNextPage()"
        >&raquo;</li>
    </ul>
</template>

<style>


</style>


<script>
export default {
    name: "PaginationBar",
    emits : ["getPage"],

    data: function () {
        return {
            numberOfPagesWanted: 10,
            booksPerPage: null,
            lastOffset: null,
        }
    },
    props: {
        query: String,
        currentPage: Number,
        totalPages: Number

    },

    methods: {
        activeIfCurrent: function(page){
            var active = (page == this.currentPage) ?  "active" : "";
            return active;

        },

        disableIfFirst: function(){

            var disable = (this.currentPage == 0) ? "disable" : "";
            return disable;
        },

        disableIfLast: function(){
            var disable = (this.currentPage == this.Pages.pop()) ? "disable" : "";
            return disable;
        },

        getPage: function(page){
            this.$.emit("getPage", this.query, page);
        },

        getPreviousPage: function(){
            if (this.currentPage == 0) {
                console.log("error");
                return;
            } 

             var offset = this.currentPage - this.booksPerPage;
            this.$.emit("getPage", this.query, offset);

        },

        getNextPage: function(){
            if (this.currentPage == this.lastOffset) {
                console.log("error");
                return;
            } 

            var offset = this.currentPage + this.booksPerPage;
            this.$.emit("getPage", this.query, offset);

        }
    },

    computed: {
        Pages: function () {
            var incrementor = Math.ceil(this.totalPages / this.numberOfPagesWanted)

            this.booksPerPage = incrementor;

            var pages = []
            pages[0] = 0
            var i
            for (i = 1; i < this.numberOfPagesWanted; i++) {
                pages[i] = pages[i - 1] + incrementor
            }

            this.lastOffset = pages[i - 1];

            // add crrent page to pages
            
            // 1 check if the crrentPage already in pages array
            var page_exists = false;
            for (i = 0; i< this.numberOfPagesWanted; i++){
                if (pages[i] == this.currentPage) {
                 page_exists = true
                }
            }


            if (page_exists) {
                return pages
            }
            
            // 2 if not add it to pages
            for (i = 0; i < this.numberOfPagesWanted - 1; i++){
                if ((this.currentPage > pages[i]) && (this.currentPage < pages[i + 1])){
                      break
                }
            }

            var j
            for (j = this.numberOfPagesWanted; j > i; j--){
                pages[j] = pages[j - 1]
                
            }
            
            pages[i + 1] = this.currentPage

            // Add classes to page
            return pages

            
        },

       


    }

}
</script>