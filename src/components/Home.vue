<template>
    <div class="container">
        <div class="mb-3 text-center results-header">
            <h2> Results </h2>
            <p> Total Items: {{items.length}}</p>
        </div>

        <p v-if="error" class="text-danger text-center">
            {{ error }}
        </p>

        <div v-if="!loading && !error && items.length > 0" class="row">
            <div v-for="item in items" :key="item.id" class="col-md-3 mb-4">
                <BookCard :item="item"/>
            </div>
        </div>
    </div>
</template>

<script>
import BookCard from './BookCard.vue';

export default {
    name: "HomePage",

    components: {
        BookCard
    },

    props: {
        items: {
            type: Array,
            required: true
        },
        loading: {
            type: Boolean,
            default: false
        },
        error: {
            type: String,
            default: ''
        }
    },

};
</script>

<style>
    .container {
        max-width: 1200px;
        padding-bottom: 2rem;
    }

    .results-header {
        margin-top: 0.5rem;
        margin-bottom: 1.5rem;
    }

</style>