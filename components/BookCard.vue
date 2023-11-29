<template>
    <v-card class="mx-auto" max-width="350">
        <v-img :src="sourceImage" height="200px" alt="Book Cover Image"></v-img>
        <v-card-title>{{ bookTitle }}</v-card-title>
        <v-card-subtitle>{{ bookAuthor }}</v-card-subtitle>
        <v-card-text>{{ bookDescription }}</v-card-text>
        <v-card-actions>
            <v-spacer></v-spacer>
            <slot name="button"></slot>
        </v-card-actions>
    </v-card>
</template>

<script>
export default {
    props: {
        bookTitle: {
            type: String,
            required: true,
        },
        bookAuthor: {
            type: String,
            required: true,
        },
        bookDescription: {
            type: String,
            required: true,
        },
        sourceImage: {
            type: String,
            default: "https://source.unsplash.com/random/?Books"
        }
    }
}
</script>