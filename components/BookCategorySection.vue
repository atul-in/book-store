<template>
        <v-col md="4">
        <h2 class="text-center mb-5">{{ bookCategoryTitle }}</h2>
        <v-row v-for="(book, index) in books" :key="index">
            <BookCard class="mb-5" :bookTitle="book.bookTitle" :bookAuthor="book.bookAuthor"
                :bookDescription="book.bookDescription">
                <template v-slot:button>
                    <v-btn class="blue--text" @click.stop="editBook(book, index)">Edit</v-btn>
                    <v-btn class="red--text" @click.stop="removeBook(book.bookCategory, index)">Remove</v-btn>
                </template>
            </BookCard>
        </v-row>
        </v-col>
</template>

<script>
import BookCard from './BookCard.vue';

export default {

    components: {
        BookCard
    },

    props: {
        bookCategoryTitle: {
            type: String
        },
        books: {
            type: Array,
            default: () => []
        }
    },

    methods: {
        removeBook(category, index) {
            this.$emit('remove-book', { category, index })
        },
        editBook(book, index) {
            this.$emit('edit-book', { book, index });
        },
    }
}
</script>