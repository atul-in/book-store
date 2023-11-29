<template>
    <v-card class="mx-auto" max-width="350">
        <v-img src="https://source.unsplash.com/random/?Books" height="200px"></v-img>
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
    props: ["bookTitle", 'bookAuthor', "bookDescription"]
}
</script>