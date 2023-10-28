<template>
            <div class="book">
                        <div src="" class="book-img" alt=""></div>
                        <h5 class="book-title">{{ book.title }}</h5>
                        <!-- <p class="book-hash" v-for="subject in subjects">{{ subject }}</p> -->
                        <p class="book-autor" v-for="author in book.author_name">{{ author }}</p>
                        <a href="#" class="book-btn">Voir</a>
            </div>
</template>

<script>
    export default {
        name: "BookCard",
        props: {
            book: Object
        },

        computed: {
            subjects: function(){
                var subs = [];
                var j = 0;
                for (var i = 0; i < this.book.subject.length, j < 3; i++){
                    if (this.book.subject[i].length < 10) {
                        subs[j] = this.book.subject[i];
                        j++;
                    }
                }

                return subs;
                // return ["subject"];
            }
        }

    }
</script>
