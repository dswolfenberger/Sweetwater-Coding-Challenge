<script setup>
import { nextTick, onBeforeUnmount, onMounted, ref, watch } from 'vue'

const props = defineProps({
  isOpen: {
    type: Boolean,
    required: true
  },
  src: {
    type: String,
    required: true
  },
  alt: {
    type: String,
    required: true
  }
})

const emit = defineEmits(['close'])

const closeButton = ref(null)

function closeLightbox() {
  emit('close')
}

// This function allows users to close the lightbox with their keyboard escape key
function handleKeydown(event) {
  if (event.key === 'Escape' && props.isOpen) {
    closeLightbox()
  }
}

// When the image is open, hide background overflow, disabling page scroll
watch(
  () => props.isOpen,
  async (isOpen) => {
    if (isOpen) {
      document.body.style.overflow = 'hidden'
      await nextTick()
      closeButton.value?.focus()
    } else {
      document.body.style.overflow = ''
    }
  }
)

// listens for keyboard input when the component opens
onMounted(() => {
  document.addEventListener('keydown', handleKeydown)
})

// stops the listener watching for the keyboard inputs
onBeforeUnmount(() => {
  document.removeEventListener('keydown', handleKeydown)
  document.body.style.overflow = ''
})
</script>

<!-- 
This component displays existing user images in a clickable lightbox
-->

<template>
<!-- 
 https://vuejs.org/guide/built-ins/teleport.html#teleport uses Vue teleport component to render the lightbox 
-->
  <teleport to="body">
    <div
      v-if="isOpen"
      class="image-lightbox"
      role="dialog"
      aria-modal="true"
      aria-label="Review image preview"
      @click.self="closeLightbox"
    >
<!--
Close button and it's functionality
-->
      <div class="image-lightbox__content">
        <button
          ref="closeButton"
          class="image-lightbox__close"
          type="button"
          aria-label="Close image preview"
          @click="closeLightbox"
        >
<!--         
Free Font Awesome SVG icon 
-->
        <span
          class="image-lightbox__close-icon"
          src="/icons/x-solid-full.svg"
          alt=""
          aria-hidden="true"
        >
        </span>
        </button>
<!--
Calls to display the selected image from the user review
-->
        <img class="image-lightbox__image" :src="src" :alt="alt" />
      </div>
    </div>
  </teleport>
</template>

<style scoped lang="scss">
@use '../../styles/variables' as *;

.image-lightbox {
  position: fixed;
  inset: 0;
  z-index: 1000;
  display: grid;
  place-items: center;
  padding: 0.5rem;
  background: $color-lightbox-background;

  &__content {
    position: relative;
    max-width: min(900px, 100%);
    max-height: 90vh;
    padding: 0.5rem;
    background: $color-background;
    border-radius: $radius-lg;
  }

  &__close {
    position: absolute;
    top: 0.75rem;
    right: 0.75rem;
    width: 2.25rem;
    height: 2.25rem;
    border: 0;
    border-radius: 999px;
    background: $sw-blue;
    color: $color-text-inverted;
    font-size: 1.5rem;
    line-height: 1;
    cursor: pointer;
   
    &:hover {
      background: $sw-blue-hover;
    }

    &:focus {
      outline: $focus-border solid $sw-black;
      outline-offset: $focus-border-offset;
    }
  }

  &__close-icon {
  display: block;
  width: 1rem;
  height: 1rem;
  margin: auto;
  background-color: $color-background;
  mask: url('/icons/x-solid-full.svg') center / contain no-repeat;
  -webkit-mask: url('/icons/x-solid-full.svg') center / contain no-repeat;
  }

  &__image {
    max-width: 100%;
    max-height: 80vh;
    object-fit: contain;
    border-radius: $radius-md;
  }
}
</style>