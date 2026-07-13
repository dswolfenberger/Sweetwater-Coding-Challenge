<script setup>
import { ref, computed } from 'vue'
import StarRating from './StarRating.vue'
import ImageLightbox from './ImageLightbox.vue'

const props = defineProps({
  review: {
    type: Object,
    required: true
  }
})

const isExpanded = ref(false)
const isLightboxOpen = ref(false)

// watches for the need to add the read more button/truncate
const shouldTruncate = computed(() => {
  return props.review.description && props.review.description.length > 200
})

function toggleExpanded() {
  isExpanded.value = !isExpanded.value
}

function openLightbox() {
  isLightboxOpen.value = true
}

function closeLightbox() {
  isLightboxOpen.value = false
}
</script>

<!-- 
This component diplays the existing user review data and ratings
-->

<template>
  <article class="review-card">
    <h2>{{ review.title }}</h2>
<!-- 
Displays the review's rating using the StarRating component 
-->
    <StarRating :rating="review.starRating" />

      <p class="review-card__description" :class="{ 'review-card__description--clamped': shouldTruncate && !isExpanded }">{{ review.description }}</p>

<!--
Truncates long reviews and allows the user to expand or collapse the text
-->
    <button 
      v-if="shouldTruncate" 
      class="review-card__read-more" 
      type="button" 
      :aria-expanded="isExpanded" 
      @click="toggleExpanded">
        {{ isExpanded ? 'Show less' : 'Read more' }}
    </button>

      <p class="review-card__user">by {{ review.user }}</p>

    <button 
      v-if="review.imageUrl" 
      class="review-card__image-button" 
      type="button" 
      :aria-label="`View larger image attached to ${review.user}'s review`" 
      @click="isLightboxOpen = true">
        <img class="review-card__image" :src="review.imageUrl" :alt="`Product image attached to ${review.user}'s review`"/>
    </button>
<!-- 
Opens images attached to a review in a lightbox using ImageLightbox component    
-->
    <ImageLightbox 
      v-if="review.imageUrl" 
      :is-open="isLightboxOpen" 
      :src="review.imageUrl" 
      :alt="`Larger product image attached to ${review.user}'s review`" 
      @close="isLightboxOpen = false"
    />
  </article>
</template>

<style scoped lang="scss">
@use '../../styles/variables' as *;

.review-card {
  padding: 3rem;
  background: $color-card;
  border-radius: $radius-lg;

  h2 {
    margin: 0;
    font-size: 1.25rem;
    font-weight:500;
  }

  &__description {
    margin: 1rem 0 0.5rem;
    line-height: 1.45;
    font-size: 1rem;
    
    &--clamped {
      display: -webkit-box;
      line-clamp: 4;
      -webkit-line-clamp: 4;
      -webkit-box-orient: vertical;
      overflow: hidden;
    }
  }

  &__read-more {
    display: inline;
    width: auto;
    margin: 0 0 1.25rem;
    padding: 0;
    border: 0;
    background: transparent;
    color: $sw-blue;
    font-weight: 700;
    font-size:0.8rem;
    text-decoration: underline;
    cursor: pointer;
   
    &:hover {
      color: $sw-blue-hover;
    }
  }

  &__user {
    margin: 1rem 0;
    font-size:0.8rem;
    color: $color-muted;
  }

  &__image {
    width: 72px;
    height: 72px;
    object-fit: cover;
    border-radius: $radius-md;
  }

  &__image-button {
    width: fit-content;
    padding: 0;
    border: 0;
    background: transparent;
    cursor: pointer;
    
    &:focus {
      outline: $focus-border solid $sw-black;
      outline-offset:  $focus-border-offset;
      border-radius: $radius-md;
    }
  }
}
</style>