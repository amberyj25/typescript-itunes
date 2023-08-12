<template>
  <div class="album">
    <div class="album-name-title">專輯名稱: </div>
    <div class="album-name">{{ album.collectionName }}</div>
    <div class="album-img-box">
      <img :src="album.artworkUrl100" alt="img" class="album-img"/>
    </div>
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

<style>
.album {
  margin: 15px;
}
.album-name-title {
  font-size: 20px;
}
.album-name {
  height: 28px;
  font-size: 16px;
}
.album-img-box {
  height: 150px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.album-img {
  width: 125px;
  height: 100px;
}
</style>
