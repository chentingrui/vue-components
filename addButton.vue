<template>
  <span class="hr-add-btn" @click="onClick">
    <i class="fa fa-plus"></i>
    <span>{{text}}</span>
  </span>
</template>

<script>
export default {
  props: {
    text: String
  },
  methods: {
    onClick() {
      this.$emit('click')
    }
  }
}
</script>
<style scoped>
.hr-add-btn{
  color: #5ba54b;
  font-size: 14px;
  line-height: 20px;
  cursor: pointer;
  background-size: 16px;
}
.hr-add-btn i{
  padding-right: 4px;
}
</style>