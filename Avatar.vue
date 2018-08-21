<template>
<div class="hr-avatar">
  <img v-lazy="imgUrl" class="hr-avatar-img" :width="size" :height="size" />
  <div v-if="notification" class="hr-avatar-notification"></div>
</div>
</template>

<script>
import defaultAvatar from './default_avatar.png'

export default {
  props: {
    notification: false,
    size: '',
    src: ''
  },
  computed: {
    imgUrl() {
      let baseURL = '/'
      if (window.location.host.indexOf('localhost') > -1) {
        baseURL = 'http://10.61.213.105/'
      }

      let imageURL = this.src ? `${baseURL}StaticResource${this.src}` : ''

      return {
        src: imageURL || defaultAvatar,
        error: defaultAvatar,
        loading: defaultAvatar
      }
    }
  }
}
</script>
<style scoped>
.hr-avatar {
  position: relative;
  padding: 0;
  display: inline-block;
}

.hr-avatar-img {
  border-radius: 50%;
  margin: 0;
  object-fit: cover;
  vertical-align: middle;
}

.hr-avatar-notification {
  width: 9px;
  height: 9px;
  border-radius: 50%;
  background: rgb(236, 84, 95);
  position: absolute;
  right: 0px;
  top: 0px;
  box-shadow: rgba(0, 0, 0, 0.5) 0px 3px 4px 0px;
}
</style>
