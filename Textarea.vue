<template>
  <div class="textarea-wrap">
    <textarea :class="{'borderless':borderless, 'empty': currentValue.value=='', 'request-feed-text': requestFeedText, 'feedback' : isFeedback }" class="textarea" ref="textarea" @change="onChange" :placeholder="placeholder" :maxlength="maxlength" v-model="currentValue.value" :style="styles"></textarea>
  </div>
</template>
<script>

export default {
  props: {
    placeholder: String,
    maxlength: Number,
    value: Object,
    borderless: Boolean,
    requestFeedText: Boolean,
    focus: Boolean,
    styles: Object,
    enableHTML: false, // Flag that defines whether HTML characters should be accepted
    isFeedback: false // For feedback having different style of placeholder
  },
  data () {
    return {
    }
  },
  computed: {
    currentValue: {
      get () {
        if (!this.enableHTML) {
          this.value.value = this.value.value
        }
        return this.value
      },
      set (val) {
        this.$emit('input', val)
      }
    }
  },
  mounted () {
    this.makeExpandingArea(this.$refs.textarea)
    this.currentValue.left = this.leftCount(this.currentValue.value.length)
    if (this.focus) {
      this.$refs.textarea.focus()
    }
  },
  methods: {
    onChange (e) {
      this.$emit('change', e)
    },
    makeExpandingArea (el) {
      function setStyle (el) {
        el.style.height = 'auto'
        el.style.height = el.scrollHeight + 2 + 'px'
      }
      function delayedResize(el) {
        window.setTimeout(function () {
          setStyle(el)
        }, 0)
      }
      setStyle(el)

      if (el.addEventListener) {
        el.addEventListener('input', function () {
          setStyle(el)
        }, false)
      } else if (el.attachEvent) {
        el.attachEvent('onpropertychange', function () {
          setStyle(el)
        })
        setStyle(el)
      }

      if (window.VBArray && window.addEventListener) {
        el.attachEvent('onkeydown', function () {
          var key = window.event.keyCode
          if (key === 8 || key === 46) delayedResize(el)
        })

        el.attachEvent('oncut', function () {
          delayedResize(el)
        })
      }
    },
    leftCount (length) {
      let _left = this.maxlength - length
      let _msg = ''
      if (_left === 0) {
        _msg = 'You have reached the maximum limit'
      } else if (_left === 1) {
        _msg = _left + ' character left'
      } else if (_left <= 50) {
        _msg = _left + ' characters left'
      }
      return _msg
    }
  },
  watch: {
    'currentValue.value': function (val) {
      this.currentValue.left = this.leftCount(val.length)
    }
  }
}
</script>


<style scoped lang="less">
.textarea-wrap{
  line-height: 0;
}

.textarea{
  font-size: 15px;
  font-family: Ubuntu-Regular;
  width: 100%;
  line-height: 20px;
  box-sizing: border-box;
  outline: 0;
  border: 1px solid #a0b3d6;
  min-height: 30px;
  padding: 5px 50px 5px 5px;
  outline: 0;
  border: none;
  word-break: break-all;
  overflow-x: hidden;
  overflow-y: auto;
  resize: none;
  -webkit-user-modify: read-write-plaintext-only;
  &.borderless {
    border: none;
  }
  &.empty {
    color: #d7d9dd;
  }
  &.request-feed-text{
    font-family:ubuntu-regular;
    color:rgb(41,24,61);
    font-size:15px;
    line-height:20px;
    padding:0px 14px 0px 0px;
  }
}

.feedback::-webkit-input-placeholder {
    /* feedback specific placeholder style*/
    color : rgb(215, 217, 220);
}
</style>
