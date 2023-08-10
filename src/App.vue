<template>
  <input type="text" id="searchInput" v-model="searchText" />
  <button @click="searchItunes(searchText)">Search</button>
</template>

<script lang="ts">
import { defineComponent, ref, reactive } from 'vue'

export default defineComponent({
  name: 'App',
  setup () {
    const albums = reactive({ data: {} })
    const searchText = ref('')
    const searchItunes = (search: string) => {
      console.log('data', albums)
    }

    return {
      searchItunes,
      searchText,
      albums
    }
  }
})
</script>
