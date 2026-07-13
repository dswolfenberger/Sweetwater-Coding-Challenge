<script setup>
//importing primary components, the review form on the left and review list on the right, which are both called below and aligned in a responsive grid.
import ReviewForm from './components/review/ReviewForm.vue'
import ReviewList from './components/review/ReviewList.vue'
import reviews from './data/reviews.json'

const reviewItems = reviews
</script>

<template>
  <main class="review-page">
    <div class="review-page__layout">
      <ReviewForm />
      <ReviewList :reviews="reviewItems" />
    </div>
  </main>
</template>

<style scoped lang="scss">
.review-page {
  max-width: 1080px;
  margin: 0 auto;
  padding: 3rem 1rem;

  &__layout {
    display: grid;
    gap: 1.75rem;

    @media (min-width: 900px) {
      grid-template-columns: 1fr 1fr;
      align-items: start;
    }
  }
}
</style>