<script setup>
import { reactive, ref } from 'vue'
import RatingInput from './RatingInput.vue'

/*
Data structure for components:
  title
  description
  starRating
  imageUrl
*/

const form = reactive({
  title: '',
  description: '',
  starRating: 0,
  imageUrl: ''
})

/*
Code to watch for files and display proper values for inputs
*/
const fileInput = ref(null)
const selectedFileName = ref('No file chosen...')

function selectFile() {
  fileInput.value?.click()
}

function handleFileChange(event) {
  const file = event.target.files?.[0]

  selectedFileName.value = file
    ? file.name
    : 'No files chosen...'
}
</script>

<!--
This component displays the inputs for users to add new reviews and ratings.
-->

<template>
  <section class="review-form" aria-labelledby="review-form-title">
    <h1 id="review-form-title">Submit Your Review</h1>

    <form>
      <div class="review-form__field">
        <label for="review-title">
          Review Title
          <span
            class="review-form__required"
            aria-hidden="true"
          >
            *
          </span>
        </label>

        <input
          id="review-title"
          v-model="form.title"
          name="title"
          type="text"
          required
        />
      </div>

      <div class="review-form__field">
        <RatingInput
          v-model="form.starRating"
          label="Your Rating"
          required
        />
      </div>

      <div class="review-form__field">
        <label for="review-body">
          Review
          <span
            class="review-form__required"
            aria-hidden="true"
          >
            *
          </span>
        </label>

        <textarea
          id="review-body"
          v-model="form.description"
          name="body"
          rows="8"
          required
        ></textarea>
      </div>

      <!--
      Took a break to review button accessibility outlined in the Vue docs:
      https://vuejs.org/guide/best-practices/accessibility.html#buttons
      -->

      <div class="review-form__field">
        <label id="review-image-label" for="review-image">
          Add Image
          <span class="review-form__optional">
            (optional)
          </span>
        </label>

        <input
          id="review-image"
          ref="fileInput"
          class="review-form__file-input"
          name="image"
          type="file"
          accept="image/*"
          tabindex="-1"
          @change="handleFileChange"
        />

        <div class="review-form__file-control">
          <button
            class="review-form__file-button"
            type="button"
            aria-describedby="review-image-label"
            @click="selectFile"
          >
            Select Files
          </button>

          <span
            class="review-form__file-name"
            role="status"
            aria-live="polite"
          >
            {{ selectedFileName }}
          </span>
        </div>
      </div>

      <button type="submit">
        Submit Review
      </button>
    </form>
  </section>
</template>

<style scoped lang="scss">
@use '../../styles/variables' as *;

.review-form {
  padding: 3rem;
  background: $color-card;
  border-radius: $radius-lg;

  /*
  Added code to improve the user experience by keeping the form sticky.
  */
  @media (min-width: 900px) {
    position: sticky;
    top: 2rem;
  }

  h1 {
    margin: 0 0 1.5rem;
    font-size: 1.25rem;
    font-weight: 500;
  }

  &__field {
    display: grid;
    gap: 0.25rem;
    margin-bottom: 1.25rem;

    textarea {
      height: 6rem;
    }
  }

  &__required {
    color: $sw-red;
    font-size: 1rem;
  }

  &__optional {
    color: $color-muted;
    font-size: 0.8rem;
    font-weight: 300;
  }

  &__file-input {
    display: none;
  }

  &__file-control {
    display: flex;
    gap: 1rem;
    padding:0.5rem;
    border: 1px solid $color-border;
    border-radius: $radius-md;
    background: $color-background;
  }

  &__file-button {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 2.25rem;
    max-width:10rem;
    margin: 0;
    padding: $space-md;
    border: 1px solid $color-border;
    border-radius: $radius-sm;
    background: $color-file-button;
    color: $color-text;
    font-size: 1rem;
    font-weight: 500;
    cursor: pointer;

    &:hover {
      background: $color-file-button-hover;
    }

    &:focus {
      outline: $focus-border solid $sw-black;
      outline-offset: $focus-border-offset;
    }
  }

  &__file-name {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0 1rem;
    overflow: hidden;
    color: $color-muted;
    font-size: 1rem;
    font-weight: 500;
    text-align: center;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
}

label {
  font-weight: 500;
}

input,
textarea {
  width: 100%;
  min-height: 3.5rem;
  padding: 0.8rem;
  border: 1px solid $color-border;
  border-radius: $radius-md;
  background: $color-background;

  &:focus-visible {
    outline: $focus-border solid $sw-black;
    outline-offset: $focus-border-offset;
  }
}

textarea {
  resize: vertical;
}

button {
  width: 100%;
  margin-top: 0.5rem;
  padding: 1.2rem;
  border: 0;
  border-radius: 999px;
  background: $sw-blue;
  color: $color-text-inverted;
  font-weight: 700;
  cursor: pointer;

  &:hover {
    background: $sw-blue-hover;
  }

  &:focus-visible {
    outline: $focus-border solid $sw-black;
    outline-offset: $focus-border-offset;
  }
}
</style>