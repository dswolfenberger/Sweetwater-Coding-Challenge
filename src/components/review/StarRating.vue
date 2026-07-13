<script setup>
defineProps({
  rating: {
    type: Number,
    required: true,
    validator: (value) => value >= 0 && value <= 5
  }
})
</script>

<!--
This component displays existing star ratings.
-->

<template>
  <span
    class="star-rating"
    :aria-label="`${rating} out of 5 stars`"
  >
    <i
      v-for="star in 5"
      :key="star"
      aria-hidden="true"
      class="star-rating__star"
      :class="
        star <= rating
          ? 'star-rating__star--filled'
          : 'star-rating__star--empty'
      "
    ></i>
  </span>
</template>

<style scoped lang="scss">
@use '../../styles/variables' as *;

.star-rating {
  display: inline-flex;
  align-items: center;
  gap: 0.15rem;
  margin: 0.25rem 0 0;

 &__star {
  display: inline-block;
  width: 1rem;
  height: 1rem;
  background-color: $color-star;
  mask: url('/icons/star-filled.svg') center / contain no-repeat;
  -webkit-mask: url('/icons/star-filled.svg') center / contain no-repeat;
}
  &__star--filled {
    color: $color-star;
    mask-image: url('/icons/star-filled.svg');
    -webkit-mask-image: url('/icons/star-filled.svg');
  }

  &__star--empty {
    color: $color-star-empty;
    mask-image: url('/icons/star-empty.svg');
    -webkit-mask-image: url('/icons/star-empty.svg');
  }

}
</style>