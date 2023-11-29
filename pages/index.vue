<template>
    <div>

        <v-row>
            <v-col md="4">
                <h2 class="text-center mb-5">Recently Read Books</h2>
                <v-row v-for="(book, index) in recentBooks" :key="index">
                    <BookCard 
                        class="mb-5" 
                        :bookTitle="book.bookTitle" 
                        :bookAuthor="book.bookAuthor"
                        :bookDescription="book.bookDescription"
                    >
                        <template v-slot:button>
                            <v-btn class="blue--text" @click.stop="editBook(book, index)">Edit</v-btn>
                            <v-btn class="red--text" @click.stop="removeBook(book.bookCategory, index)">Remove</v-btn>
                        </template>
                    </BookCard>
                </v-row>
            </v-col>
            <v-col md="4">
                <h2 class="text-center mb-5">Favourite Books</h2>
                <v-row v-for="(book, index) in favouriteBooks" :key="index">
                    <BookCard 
                        class="mb-5" 
                        :bookTitle="book.bookTitle" 
                        :bookAuthor="book.bookAuthor"
                        :bookDescription="book.bookDescription"
                    >
                        <template v-slot:button>
                            <v-btn class="blue--text" @click.stop="editBook(book, index)">Edit</v-btn>
                            <v-btn class="red--text" @click.stop="removeBook(book.bookCategory, index)">Remove</v-btn>
                        </template>
                    </BookCard>
                </v-row>
            </v-col>
            <v-col md="4">
                <h2 class="text-center mb-5">Best Books</h2>
                <v-row v-for="(book, index) in bestBooks" :key="index">
                    <BookCard 
                        class="mb-5" 
                        :bookTitle="book.bookTitle" 
                        :bookAuthor="book.bookAuthor"
                        :bookDescription="book.bookDescription"
                    >
                        <template v-slot:button>
                            <v-btn class="blue--text" @click.stop="editBook(book, index)">Edit</v-btn>
                            <v-btn class="red--text" @click.stop="removeBook(book.bookCategory, index)">Remove</v-btn>
                        </template>
                    </BookCard>
                </v-row>
            </v-col>
        </v-row>

        <BookModal />

    </div>
</template>

<script>
import BookCard from '../components/BookCard.vue';
import BookModal from '../components/BookModal.vue';
import { eventBus } from '../eventBus';


export default {
    components: {
        BookCard,
        BookModal,
    },

    data() {
        return {
            recentBooks: [],
            favouriteBooks: [],
            bestBooks: []
        }
    },

    created() {
        eventBus.$on("save-book", bookData => {
            if (bookData.bookCategory === "Recently read Books") {
                this.recentBooks.push(bookData)
                this.recentBooks.sort((a, b) => b - a)
            }
            if (bookData.bookCategory === "Favourite Books") {
                this.favouriteBooks.push(bookData)
                this.favouriteBooks.sort((a, b) => b - a)
            }
            if (bookData.bookCategory === "Best Books"){
                this.bestBooks.push(bookData)
                this.bestBooks.sort((a, b) => b - a)
            }
        })
    },

    methods: {
        removeBook(category, index) {
            if (category === 'Recently read Books') {
                this.recentBooks.splice(index, 1)
            }
            if (category === 'Favourite Books') {
                this.favouriteBooks.splice(index, 1)
            }
            if (category === 'Best Books') {
                this.bestBooks.splice(index, 1)
            }
            
        },

        editBook(book, index) {
            if (book.bookCategory === "Recently read Books") {
                eventBus.$emit("open-add-book-modal", book)
                this.recentBooks.splice(index, 1)
            }
            if (book.bookCategory === "Favourite Books") {
                eventBus.$emit("open-add-book-modal", book)
                this.favouriteBooks.splice(index, 1)
            }
            if (book.bookCategory === "RBest Books") {
                eventBus.$emit("open-add-book-modal", book)
                this.bestBooks.splice(index, 1)
            }
            
        }
    }
} 
</script>