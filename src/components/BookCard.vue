<template>
  <div class="card h-100" :class="cardClass(item)">
    <div class="card-body">
      <h6 class="card-title book-title">
        {{ item.title }}
      </h6>
      <hr>
      <p class="card-text">
        Year -> {{ item.year }}
      </p>
      <hr>
      <p class="card-text">
        Published: {{ item.published ? 'Yes' : 'No' }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BookCard',
  props: {
    item: {
      type: Object,
      required: true
    }
  },
  methods: {
    cardClass(item) {
      return item.published ? 'book-card-published' : 'book-card-unpublished';
    }
  }
};
</script>

<style>
    .book-title {
        min-height: 3.5rem;
        font-size: 1rem;
    }

    .card-text {
        margin-bottom: 0.4rem;
    }

    .card.h-100 {
        border-radius: 0.75rem;
        box-shadow: 0 0.5rem 1rem rgba(0,0,0,0.15);
    }

    .book-card-unpublished {
        background-color: gray;
        color: #ffffff;
    }

    .book-card-published {
        background-color: green;
        color: #ffffff;
    }

    .card-body hr {
        margin: 0.5rem 0;
        color: black;
    }
</style>
