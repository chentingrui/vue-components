<template>
  <span class="hr-image-wrap">
    <img v-lazy="imgUrl" class="hr-image" :style="imgStyle"/>
  </span>
</template>

<script>
import defaultImage from './default_image.png'

export default {
  props: {
    size: '',
    src: ''
  },
  methods: {
    changeUnit: function (n) {
      return /%/g.test(n) ? n : `${n}px`
    }
  },
  computed: {
    imgUrl() {
      return {
        loading: defaultImage,
        src: this.src || defaultImage,
        error: defaultImage
      }
    },
    imgStyle() {
      let imgStyle = {}
      if (this.size) {
        let sizeArr = this.size.split(',')
        imgStyle.width = this.changeUnit(sizeArr[0])
        imgStyle.height = this.changeUnit(sizeArr[1])
      }
      return imgStyle
    }
  },
  created: function () {
  }
}
</script>
<style scoped>
.hr-image-wrap{
  font-size: 0;
}
.hr-image{
  vertical-align: top;
  display: inline-block;
  object-fit: cover;
}
</style>