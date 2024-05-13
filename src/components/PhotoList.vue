<script setup>
import PhotoCard from './PhotoCard.vue'

defineProps({
  photos: {
    type: Array,
    required: true
  }
})

</script>

<template>
  <div class="photo-list">
    <PhotoCard
      v-for="photo in photos"
      :key="photo.id"
      :id="photo.id"
      :photo="photo"
    />
  </div>
</template>

<style lang="scss" scoped>
.photo-list {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(2, 1fr);
  column-gap: 2rem;
  row-gap: 3.75rem;
}

</style>
