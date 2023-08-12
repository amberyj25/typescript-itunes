<template>
  <div id="app">
    <div class="container">
      <div class="search-box">
        <input type="text"
          class="singer-name"
          v-model="searchText"
          placeholder="輸入歌手名稱(ex.taylors)"
          @keydown.enter="searchItunes(searchText)" />
        <button type="button" class="btn btn-primary" @click="searchItunes(searchText)">查詢</button>
      </div>
      <div class="album-title">
        <div>歌手專輯(輸入歌手後呈現)</div>
      </div>
      <div class="row">
        <div v-for="album in albums.data.results" :key="album.artistId" class="album-box col-3">
          <AlbumsData :album="album"></AlbumsData>
        </div>
      </div>
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
      try {
        const value = await fetch(`https://itunes.apple.com/search?term=${search}&entity=album`)
        const valueToJSON = await value.json()
        albums.data = valueToJSON
      } catch (err) {
        console.log('catch', err)
      }
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
.container {
  width: 90%;
}
.search-box {
  display: flex;
  height: 60px;
  justify-content: center;
  align-items: center;
}
.singer-name {
  display: block;
  width: 200px;
  height: 30px;
  margin: 0 5px 0 0;
}
.btn {
  display: block;
  width: 75px;
  height: 35px;
}
.album-title {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 5px 0 15px 0;
}
.album-box {
  border: 2px solid black;
}
</style>
