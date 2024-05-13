<script setup>
import { ref } from 'vue'

defineProps({
  photo: {
    type: Object,
    required: true
  }
})

const open = ref(false)

</script>

<template>
  <div>
    <div class="photo-card" @click="open = true">
    <img class="photo-card_img" :src="photo.urls.small" alt="img" title="click for details">
    </div>
    <Teleport to="body">
      <div v-if="open" class="modal">
        <div class="modal_content">
          <img class="modal_img" :src="photo.urls.regular" alt="img">
          <p class="modal_text">Author: {{ photo.user.first_name }}</p>
          <p class="modal_text">Description: {{ photo.alt_description }}</p>
          <p class="modal_text">Likes: {{ photo.likes }}</p>
        </div>
        <div @click="open = false" title="click to close" class="modal_background"></div>
      </div>
    </Teleport>
  </div>  
</template>

<style lang="scss" scoped>
.photo-card {
  height: 17.5rem;
  cursor: pointer;

  &_img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
    border-radius: 1rem;
  }
}

.modal {
  position: fixed;
  display: flex;
  z-index: 999;

  &_content {
    position: fixed;
    padding: 1rem;
    z-index: 999;
    top: 5%;
    left: 50%;
    height: 90%;
    transform: translateX(-50%);
    border: 1px solid white;
    border-radius: 1.5rem;
    background-color: black;

  }

  &_text {
    text-align: center;
  }

  &_img {
    height: 85%;
    width: 100%;
    object-fit: contain;
    object-position: center;
  }

  &_background {
    position: fixed;
    z-index: 1;
    width: 100%;
    height: 100%;
    cursor: pointer;
    background-color: rgb(0 0 0 / 72%);
  }
}
</style>
