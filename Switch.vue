<template>
<span class="hr-switch" :class="`${this.classes}`" @click="onClick">
    <span class="slider"></span>
<span class="circle"></span>
</span>
</template>

<script>
export default {
  props: {
    switchValue: Number,
    disabled: false
  },
  data() {
    return {}
  },
  computed: {
    classes() {
      var classes = 'hr-switch-' + this.switchValue
      if (this.disabled) {
        classes += ' disabled'
      }
      return classes
    }
  },
  created() {},
  methods: {
    onClick() {
      if (this.switchValue !== 2) {
        this.$emit('switchclick', this.switchValue)
      }
    }
  }
}
</script>
<style scoped>
.hr-switch {
  position: relative;
  display: inline-flex;
  cursor: pointer;
  vertical-align: middle;
}

.hr-switch.disabled {
  cursor: not-allowed;
}

.hr-switch .slider {
  width: 34px;
  height: 14px;
  border: 1px solid rgb(205, 205, 205);
  border-radius: 10px;
  box-sizing: border-box;
  background: rgb(205, 205, 205);
  transition: border-color .3s, background-color .3s;
  opacity: 0.5;
}

.hr-switch .circle {
  position: absolute;
  top: -3px;
  left: -2px;
  border-radius: 50%;
  transition: transform .3s;
  width: 20px;
  height: 20px;
  background-color: rgb(162, 162, 162);
}

/*waiting*/

.hr-switch.hr-switch-2 {
  cursor: not-allowed;
}

.hr-switch.hr-switch-1 .slider {
  background: rgb(66, 46, 136);
  opacity: 0.2;
}

.hr-switch.hr-switch-1 .circle {
  background: rgb(66, 46, 136);
  opacity: 0.4;
  transform: translate3d(17px, 0, 0);
}

/*achieved*/

.hr-switch.hr-switch-2 .slider {
  background: rgb(66, 46, 136);
}

.hr-switch.hr-switch-2 .circle {
  background: rgb(66, 46, 136);
  transform: translate3d(17px, 0, 0);
}
</style>
