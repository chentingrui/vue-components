<template>
  <button @click="onClick" class="hr-btn" 
  :class="{'hr-btn-small':small, 'hr-btn-weak':weak, 'hr-btn-disable': disable}">
    <span class="hr-btn-flex">
        <slot></slot>
        <span class="hr-btn-text">{{text}}</span>
      </span>
    </button>
</template>
<script>
export default {
  data () {
    return {
    }
  },
  props: {
    text: String,
    small: Boolean,
    weak: Boolean,
    disable: Boolean
  },
  methods: {
    onClick () {
      if (!this.disable) {
        this.$emit('click')
      }
    }
  }
}
</script>
<style scoped>
.hr-btn{
  box-sizing: border-box;
  font-family: Ubuntu-Medium;
  padding: 0 21px;
  border:2px solid rgb(66, 46, 136);
  -webkit-tap-highlight-color: transparent; 
  -webkit-appearance: none;
  cursor:pointer;
  outline:none;
  display: inline-block;
  vertical-align: middle;
  position: relative;
  background: none;
  transition: all 0.3s;
}

/* hr-button size*/
.hr-btn{height: 46px; border-radius:24px; max-width: 100%;min-width: 180px; font-size: 17px;}
.hr-btn-small{height: 36px; border-radius: 18px; max-width: 100%;min-width: 100px;font-size: 14px; }

/* hr-button type*/
.hr-btn{color: rgb(66, 46, 136);}
.hr-btn-weak{background: none; font-size:15px; color: rgb(51,51,51); border: none;}
.hr-btn-disable{color: rgb(171, 165, 190); border-color: rgb(171, 165, 190);}

.hr-btn-flex{display: flex;justify-content: center;align-items: center;}
.hr-btn-flex i{margin-right: 12px;}
.hr-btn-text {overflow: hidden;white-space: nowrap; text-overflow: ellipsis; vertical-align: middle;}
</style>