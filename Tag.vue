<template>
  <button class="hr-tag">
    <span class="hr-tag-text" :title="text">{{text}}</span>
    <hr-icon class="hr-tag-icon" size="12,12,12,12" src="combinedShape.png" @click="onClick"/>
  </button>
</template>
<script>
export default {
  data () {
    return {
    }
  },
  props: ['text'],
  methods: {
    onClick () {
      this.$emit('click')
    }
  }
}
</script>
<style scoped>
.hr-tag {
  position: relative;
  box-sizing: border-box;
  font-family: Ubuntu-Medium;
  padding: 0 35px 0 21px;
  border: 1px solid rgb(228, 228, 228);
  -webkit-tap-highlight-color: transparent; 
  -webkit-appearance: none;
  cursor: pointer;
  outline: none;
  display: inline-block;
  vertical-align: middle;
  background: none;
  transition: all 0.3s;
  height: 30px; 
  border-radius: 18px; 
  max-width: 100%;
  min-width: 100px;
  font-size: 14px;
  color: rgb(51,51,51);
  overflow: hidden;
  white-space: nowrap; 
  text-overflow: ellipsis; 
  vertical-align: middle;
}

.hr-tag-icon {
  position: absolute;
  top: 0;
  bottom: 0;
  right: 10px;
  margin: auto;
}
</style>