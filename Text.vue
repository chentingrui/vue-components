<template>
  <div class="hr-text" :class="type">
    <slot />
  </div>
</template>

<script>
export default {
  props: {
    type: String
  },
  data () {
    return {}
  },
  created: function () {
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

.hr-text.layer-item-content{
  font-family: Ubuntu-Medium;
  color: rgb(51, 51, 51);
  font-size: 18px;
}

.hr-text.layer-item-title{
  font-family: Ubuntu-Medium;
  color: rgb(51, 51, 51);
  font-size: 14px;
}

.hr-text.category-label{
  font-family: Ubuntu-Bold;
  color: rgb(51, 51, 51);
  font-size: 22px;
}

.hr-text.header-label{
  color: rgb(51, 51, 51);
  font-size: 17px;
  font-family: Ubuntu-Medium;
}

.hr-text.main-content{
  font-family: Ubuntu-Regular;
  color: rgb(51, 51, 51);
  font-size: 15px;
}

.hr-text.date-stamp{
  font-family: Ubuntu-Regular;
  color: rgb(170, 180, 185);
  font-size: 14px;
}
</style>