<template>
  <div id="app">
    <input type="text"
      class="singerName"
      v-model="searchText"
      placeholder="輸入歌手名稱(ex.taylors)"
      @keydown.enter="searchItunes(searchText)" />
    <button @click="searchItunes(searchText)">查詢</button>
    <div v-for="album in albums.data.results" :key="album.artistId">
      <AlbumsData :album="album"></AlbumsData>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, reactive } from 'vue'
import { ItunesTypes } from '@/types/ItunesTypes'
import AlbumsData from '@/components/AlbumsData.vue'

export default defineComponent({
  name: 'App',
  components: {
    AlbumsData
  },
  setup () {
    const albums = reactive<{ data: ItunesTypes }>({ data: {} })
    const searchText = ref('')
    const searchItunes = async (search: string) => {
      const value = await fetch(`https://itunes.apple.com/search?term=${search}&entity=album`)
      const valueToJSON = await value.json()
      albums.data = valueToJSON
    }

    return {
      searchItunes,
      searchText,
      albums
    }
  }
})
</script>

<style>
.singerName {
  width: 200px;
  height: 20px;
}
</style>
