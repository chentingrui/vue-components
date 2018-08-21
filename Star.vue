<template>
  <div class="hr-star">
    <template v-for="v in counter">
      <hr-icon size="20,20,15,15" :src="v"></hr-icon>
    </template>
  </div>
</template>

<script>
export default {
  props: {
    score: Number
  },
  data () {
    return {
      counter: {}
    }
  },
  created: function () {
    this.counter = this.getNumber(this.score)
  },
  methods: {
    getNumber(n) {
      var arr = []
      for (var i = 0; i < 5; i++) {
        if (n >= 1) {
          arr.push('star/icoSlpStarfull.png')
        } else if (n >= 0.5) {
          arr.push('star/icoSlpStarHalf.png')
        } else {
          arr.push('star/icoSlpStar.png')
        }
        n--
      }
      return arr
    }
  }
}
</script>
<style scoped>
.hr-text.layer-title{
  font-family: Ubuntu-Bold;
  color: rgb(51, 51, 51);
  font-size: 24px;
  padding: 50px 0 0 0;
  text-align: center;
}
</style>