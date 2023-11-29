<template>
    <div>
        <!-- Add and edit book modal -->
        <v-dialog max-width="500px" :persistent="isDialogOpen || isEditDialog" v-model="isDialogOpen">
            <v-card class="p-5">
                <v-card-title>{{ isEditDialog ? 'Edit Book' : 'Add Book' }}</v-card-title>
                <v-form class="mx-5">
                    <v-select v-model="bookCategory" :items="booksCategories" label="Select a category"></v-select>
                    <v-text-field v-model="bookTitle" label="Enter Book Title"></v-text-field>
                    <v-text-field v-model="bookAuthor" label="Enter Book Author"></v-text-field>
                    <v-textarea v-model="bookDescription" label="Enter Book Description"></v-textarea>
                </v-form>
                <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn @click="isDialogOpen = false" class="blue--text">Close</v-btn>
                    <v-btn @click.stop="saveBook" class="green--text">{{ isEditDialog ? 'Save' : '+ Add Book' }}</v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
    </div>
</template>

<script>

import { eventBus } from '../eventBus';

export default {
    data() {
        return {
            isDialogOpen: false,
            isEditDialog: false,
            bookCategory: '',
            bookTitle: '',
            bookAuthor: '',
            bookDescription: '',
            booksCategories: [
                "Recently read Books",
                "Favourite Books",
                "Best Books"
            ],
        }
    },
    created() {
        eventBus.$on("open-add-book-modal", this.openBookModal)
    },

    methods: {

        openBookModal(data) {
            this.isEditDialog = !!data;
            if (data) {
                this.bookCategory = data.bookCategory;
                this.bookTitle = data.bookTitle;
                this.bookAuthor = data.bookAuthor;
                this.bookDescription = data.bookDescription;
            }
            this.isDialogOpen = true;
        },

        saveBook() {
            const bookData = {
                bookTitle: this.bookTitle,
                bookAuthor: this.bookAuthor,
                bookDescription: this.bookDescription,
                bookCategory: this.bookCategory
            }
            eventBus.$emit("save-book", bookData)
            this.resetForm()
        },

        resetForm() {
            this.bookCategory = '';
            this.bookTitle = '';
            this.bookAuthor = '';
            this.bookDescription = '';
            this.isDialogOpen = false;
        },
    }
}
</script>