<template>
    <v-dialog persistent max-width="500px" v-model="isDialogOpen">
        <v-card class="p-5">
            <v-card-title>Add Books</v-card-title>
            <v-form class="mx-5">
                <v-select v-model="bookCategory" :items="booksCategories" label="Select a category"></v-select>
                <v-text-field v-model="bookTitle" label="Enter Book Title"></v-text-field>
                <v-text-field v-model="bookAuthor" label="Enter Book Author"></v-text-field>
                <v-textarea v-model="bookDescription" label="Enter Book Description"></v-textarea>
            </v-form>
            <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn @click="handleCloseDialog" class="blue--text">Close</v-btn>
                <v-btn @click.stop="saveBook" class="green--text">+ Add Book</v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
</template>

<script>

import { eventBus } from '../eventBus';

export default {
    data() {
        return {
            isDialogOpen: false,
            bookCategory: '',
            bookTitle: '',
            bookAuthor: '',
            bookDescription: '',
            booksCategories: [
                "Recently read Books",
                "Favourite Books",
                "Best Books"
            ]
        }
    },
    created() {
        eventBus.$on("open-add-book-modal", data => {
            if (data) {
                this.bookCategory = data.bookCategory
                this.bookTitle = data.bookTitle
                this.bookAuthor = data.bookAuthor
                this.bookDescription = data.bookDescription
            }
            this.isDialogOpen = true
        })
    },

    methods: {
        saveBook() {
            let cardData = {
                bookTitle: this.bookTitle,
                bookAuthor: this.bookAuthor,
                bookDescription: this.bookDescription,
                bookCategory: this.bookCategory
            }
            eventBus.$emit("save-book", cardData)
            this.bookCategory = ''
            this.bookTitle = ''
            this.bookAuthor = ''
            this.bookDescription = ''
            this.isDialogOpen = false
        },

        handleCloseDialog() {
            this.isDialogOpen = false
        }
    }
}
</script>