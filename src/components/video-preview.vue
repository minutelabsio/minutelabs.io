<template lang="pug">
video(autoplay, autobuffer, loop, muted, playsinline)
  source(v-for="file in fileList", :src="file.url", :type="file.type")
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
  }
  , data: () => ({
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
  }
}
</script>

<style lang="sass" scoped>
</style>
