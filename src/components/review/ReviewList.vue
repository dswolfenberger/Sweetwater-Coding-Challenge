<script setup>
import ReviewCard from './ReviewCard.vue'

defineProps({
  reviews: {
    type: Array,
    required: true
  }
})
</script>

<!-- 
This component displays the existing user review data in an organized grid view
-->

<template>
  <section class="review-list" aria-label="Customer reviews">
    <ReviewCard
      v-for="(review, index) in reviews"
      :key="`${review.user}-${index}`"
      :review="review"
    />
  </section>
</template>

<style scoped lang="scss">

.review-list {
  display: grid;
  gap: 1.75rem;
}
</style>