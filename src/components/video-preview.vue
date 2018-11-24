<template lang="pug">
video(autoplay, loop, muted, playsinline)
  source(v-for="file in fileList", :src="file.url", :type="file.type")
</template>

<script>
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
      return this.files.map( url => {
        let ext = url.match(/\.([^.]+)$/)[1]
        let type = `video/${ext}`
        return {
          url
          , ext
          , type
        }
      })
    }
  }
  , methods: {
  }
}
</script>

<style lang="sass" scoped>
</style>
