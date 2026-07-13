<script setup>
import { useId } from 'vue'

const props = defineProps({
  modelValue: {
    type: Number,
    required: true,
    validator: (value) =>
      Number.isInteger(value) && value >= 0 && value <= 5
  },
  label: {
    type: String,
    default: 'Select a rating'
  },
  required: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['update:modelValue'])

// This will create a unique ID for rating components so more than one can appearr on the page
const ratingGroupId = useId()


function getStarId(star) {
  return `${ratingGroupId}-star-${star}`
}

function setRating(rating) {
  if (rating !== props.modelValue) {
    emit('update:modelValue', rating)
  }
}
</script>

<template>
  <fieldset class="rating-input">
    <legend class="rating-input__legend">
      {{ label }}

      <span
        v-if="required"
        class="rating-input__required"
        aria-hidden="true"
      >
        *
      </span>
    </legend>

    <div class="rating-input__stars">
      <template v-for="star in 5" :key="star">
        <input
          :id="getStarId(star)"
          class="rating-input__control"
          type="radio"
          :name="`${ratingGroupId}-review-rating`"
          :value="star"
          :checked="modelValue === star"
          :required="required"
          @change="setRating(star)"
        />

        <label
          class="rating-input__star"
          :class="{
            'rating-input__star--selected': star <= modelValue
          }"
          :for="getStarId(star)"
        >
          <span class="rating-input__label-text">
            {{ star }} out of 5 stars
          </span>

          <span
            class="rating-input__icon"
            aria-hidden="true"
          ></span>
        </label>
      </template>
    </div>

    <p
      class="rating-input__status"
      aria-live="polite"
      aria-atomic="true"
    >
      {{
        modelValue
          ? `${modelValue} out of 5 stars selected`
          : 'No rating selected'
      }}
    </p>
  </fieldset>
</template>

<style scoped lang="scss">
@use '../../styles/variables' as *;

.rating-input {
  padding: 0;
  margin: 0;
  border: 0;

  &__legend {
    padding: 0;
    margin-bottom: 0.5rem;
    font-weight: 500;
  }

  &__required {
    color: $sw-red;
  }

  // hides the native controls while keeping them accessible
  &__control,
  &__label-text {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    border: 0;
    white-space: nowrap;
    clip-path: inset(50%);
  }

  &__stars {
    display: inline-flex;
    align-items: center;
    gap: 0.05rem;
  }

  &__star {
    display: grid;
    width: 1.5rem;
    height: 1.5rem;
    padding: 0;
    border: 0;
    border-radius: $radius-md;
    cursor: pointer;
    place-items: center;
  }

  &__icon {
    position: relative;
    width: 1.25rem;
    height: 1.25rem;

// Uses the Font Awesome SVG in a mask
    &::before,
    &::after {
      position: absolute;
      inset: 0;
      content: '';
      mask: url('/icons/star-filled.svg') center / contain no-repeat;
      -webkit-mask: url('/icons/star-filled.svg') center / contain no-repeat;
    }

    &::before {
      background-color: $color-star;
    }

    &::after {
      background-color: $color-card;
      transform: scale(0.72);
    }
  }

  &__star--selected &__icon::after {
    background-color: $color-star;
  }

  &__star:hover &__icon::before,
  &__star:hover &__icon::after {
    background-color: $color-star;
  }

  &__star:hover &__icon::after {
    transform: scale(1);
  }

// Shows keyboard focus around the visible star label
  &__control:focus-visible + &__star {
    outline: $focus-border solid $sw-black;
    outline-offset: $focus-border-offset;
  }

  &__status {
    margin: 0.4rem 0 0;
    color: $color-muted;
    font-size: 0.8rem;
  }
}
</style>