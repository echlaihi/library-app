<template>
            <div class="book">
                        <!-- <div  class="" alt="">{{ book.isbn ? ""}}</div> -->

                        <!-- image : {{  cover }} -->
                        <img :src="cover" class="book-img"/>
                        <h5 class="book-title">{{ book.title }}</h5>
                        <!-- <p class="book-hash" v-for="subject in subjects">{{ subject }}</p>
                        <p class="book-author" v-for="author in book.author_name">{{ author }}</p> -->
                        <a href="#" class="book-btn">Voir</a>
            </div>
</template>

<script>

    import axios from 'axios';

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
            },

            cover: function(){
               
                var keys = [
                    {
                        name: "isbn",
                        value: null
                    },

                    {
                        name: "oclc",
                        value: null
                    },

                    {
                        name: "lccn",
                        value: null
                    }
                ]

                keys[0].value = this.book.isbn ? this.book.isbn[0] : false;
                keys[1].value = this.book.oclc ? this.book.oclc[0] : false;
                keys[2].value = this.book.lccn ? this.book.lccn[0] : false;

                // return keys;

                for(var i = 0; i < keys.length; i++)
                {
                    if (keys[i].value) {

                        // trying to check if the image is available;
                        // axios
                        // .get(`https://covers.openlibrary.org/b/${keys[i].name}/${keys[i].value}.json`)
                        // // .get('https://covers.openlibary.org/b/isbn/9780747593768.json')
                        // .then(resp => {
                        //     return resp;
                        // })
                        // .catch(error => {
                        //     return error;
                        // })

                        return `https://covers.openlibrary.org/b/${keys[i].name}/${keys[i].value}-M.jpg`;
                    }
                }


            },

            image: function(){

                var id  = this.book.cover_i ? this.book.cover_i : false;
                // if (!id) alert("no id");

            }
        }

    }
</script>
