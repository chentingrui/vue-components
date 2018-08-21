<template>
<div class="dropdown">
  <input class="dropdown__value" :class="arrowSize" :value="description" :placeholder="placeholder"
  :readonly="readOnly" type="text" :style="styles" />
  <ul class="dropdown__options" :class="{'expand':expand, 'hide': !expand}">
    <li v-for="option in optionsToDisplay" @click="setValue(option)"
    class="dropdown-option">{{option.description}}</li>
  </ul>
</div>
</template>

<script>
import _ from 'lodash'
export default {
  props: {
    placeholder: String,
    options: Array,
    value: {
      type: Object,
      default() {
        return {
          description: '',
          value: undefined
        }
      }
    },
    readOnly: {
      type: Boolean,
      default () {
        return true
      }
    },
    arrow: {
      type: String,
      default: 'small'
    },
    styles: {
      type: Object,
      default() {
        return {}
      }
    }
  },
  computed: {
    arrowSize() {
      switch (this.arrow) {
        case 'small':
          return 'dropdown__value--small'
        case 'big':
          return 'dropdown__value--big'
      }
    },
    optionsToDisplay() {
      return _.filter(this.options, o => o.description !== this.description)
    }
  },
  data() {
    return {
      currentValue: undefined,
      description: '',
      expand: false
    }
  },
  methods: {
    setValue(option) {
      this.description = option.description
      this.currentValue = option.value

      this.$emit('input', option)
    },
    isDropdownClicked(e) {
      if (e.target.parentNode === this.$el || e.target.parentNode.parentNode === this.$el) {
        var expand = this.expand
        this.expand = !expand
      } else {
        this.expand = false
      }
    },
    addEventListener() {
      document.getElementById('app').addEventListener('click', this.isDropdownClicked)
    },
    removeEventListener() {
      document.getElementById('app').removeEventListener('click', this.isDropdownClicked)
    }
  },
  created() {
    this.description = this.value.description
    this.addEventListener()
  },
  destroyed() {
    this.removeEventListener()
  }
}
</script>

<style scoped lang="scss">
.dropdown {
    width: 294px;
    height: 40px;
    line-height: 40px;
    text-align: left;
    position: relative;
    cursor: pointer;
    display: inline-block;
    &__value {
        font-family: Ubuntu-Medium;
        font-size: 14px;
        width: 100%;
        display: block;
        border-bottom: 1px solid #333;
        background-repeat: no-repeat;
        background-position: right center;
        border: none;
        border-bottom: 1px solid #333333;
        outline: none;
        height: 40px;
        padding: 0;
        cursor: pointer;

        &--big {
          background-image: url("../dropdown/icoFormDropdown@2x.png");
          background-size: auto 7px;
        }

        &--small {
          background-image: url("../dropdown/icoFormDropdown.png");
          background-size: auto 7px;
        }
    }
    &__options {
        font-family: Ubuntu-Medium;
        position: absolute;
        top: 41px;
        left: 0;
        list-style: none;
        max-height: 239px;
        overflow-y: auto;
        z-index: 1000;
        background-color: #fff;
        box-shadow: 0 2px 7px 0 rgba(0,0,0,0.3);
        width: 100%;
        &.hide {
            display: none;
        }
        &.expand {
            display: block;
        }
        li {
            font-size: 14px;
            line-height: 40px;
            padding: 0 22px;
            z-index: 50px;
            &:active {
                background-color: #aba5be;
            }
        }
    }
}
</style>
