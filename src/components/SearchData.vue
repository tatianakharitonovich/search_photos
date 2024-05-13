<script setup>
import PhotoList from './PhotoList.vue'
import Pagination from './Pagination.vue'
import { ref, watch } from 'vue'
import { debounce } from 'lodash'

const loading = ref(false)
const photos = ref(null)
const pages = ref(null)
const currentPage = ref(1)
const error = ref(null)
const searchQuery = ref(null)

async function fetchData() {
  error.value = null
  loading.value = true

  fetch(`https://api.unsplash.com/search/photos?query=${searchQuery.value}&page=${currentPage.value}`, {
    headers: {
      Authorization: "Client-ID _FOXPKDW5sEAlWEaqMuJOj6zLbxGwFl9S7PPSyHCnqs"
    },
  })
    .then((response) => {
      response.json().then((data) => {
        photos.value = data.results
        pages.value = data.total_pages
      });
    })
    .catch((err) => {
      error.value = err
      console.log(error.value)
    })
    .finally(()=>{
      loading.value = false
    });
}

watch(searchQuery, debounce(() => {
  pages.value = null
  currentPage.value = 1
  fetchData()
}, 600))

watch(currentPage, debounce(() => {
  photos.value = null
  fetchData()
}, 200))

function refreshCurrentPage(pageNumber) {
  currentPage.value = pageNumber
}

</script>

<template>
  <section class="search-data">
    <input
      v-model="searchQuery"
      type="text"
      class="search-data_input"
      placeholder="Enter a keyword to search"
    />
    <div v-if="pages">
      <Pagination
        :totalItems="pages"
        :itemsPerPage="10"
        @change="refreshCurrentPage"
      />
    </div>
    <div v-if="loading">
      <h3>Loading...</h3>
    </div>
    <div v-else-if="error">
      <h3>Error message {{ error.message }}</h3>
    </div>
    <div v-else-if="photos">
      <PhotoList :photos="photos" />
    </div>
    <div v-else>
      <h3>There is no data</h3>
    </div>
  </section>
  
</template>

<style scoped lang="scss">

.search-data {
  display: flex;
  flex-direction: column;
  gap: 2rem;

  &_input {
    max-width: 37rem;
    padding: 0.5rem 1rem;
    font-size: 1.2rem;
    border-radius: 1rem;
  }
}

h3 {
  font-weight: 500;
  font-size: 1.5rem;
  position: relative;
}

</style>
