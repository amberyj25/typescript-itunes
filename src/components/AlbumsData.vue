<template>
  <div>
    <h2>專輯名稱: {{ album.collectionName }}</h2>
    <img :src="album.artworkUrl100" alt="picture"/>
    <h4>價格: {{ album.collectionPrice }}</h4>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'AlbumsData',
  props: {
    album: {
      type: Object,
      required: true
    }
  },
  setup () {
    return {}
  }
})
</script>
