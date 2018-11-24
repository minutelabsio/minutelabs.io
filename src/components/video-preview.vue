<template lang="pug">
.preview
  video(v-if="!useFallback", autoplay, autobuffer, loop, muted, playsinline)
    source(
      v-for="(file, index) in fileList"
      , :src="file.url"
      , :type="file.type"
      , @error="(index === fileList.length - 1) && fallback()"
    )
  img(v-if="useFallback", :src="poster")
</template>

<script>
import _sortBy from 'lodash/sortBy'

const typeOrder = [
  'webm'
  , 'mp4'
]
function extSort( file ){
  let idx = typeOrder.indexOf(file.ext)
  return idx > -1 ? idx : Infinity
}

export default {
  name: 'video-preview'
  , props: {
    files: Array
    , poster: String
  }
  , data: () => ({
    useFallback: false
  })
  , components: {
  }
  , computed: {
    fileList(){
      let files = this.files.map( url => {
        let ext = url.match(/\.([^.]+)$/)[1]
        let type = `video/${ext}`
        return {
          url
          , ext
          , type
        }
      })
      return _sortBy(files, extSort)
    }
  }
  , methods: {
    fallback(){
      this.useFallback = true
    }
  }
}
</script>

<style lang="sass" scoped>
</style>
