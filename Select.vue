
<template>
    <div>
      <div class="selct" @click.stop="onArrow" @blur="isOpen=false" tabindex="1">
        <div class="select-inner">
          <div class="label" v-show="labelValue">{{labelValue}}</div>
          <div class="title">
            <span v-if="value.displayValue">{{value.displayValue}}</span>
            <span class="placeholder" v-else>{{placeholder}}</span>
          </div>
        
          <div class="arrow">
           <i class="fa fas fa-angle-up" :class="{'rotate': !isOpen, 'rotate-back': isOpen}"></i>
          </div>
        </div>
        <div class="select-items" v-if="isOpen">
          <div class="select-list">
            <ul>
              <li v-for="item in value.list" :key="item.id" @click="onChange(item)">{{item.value}}</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
</template>
<script>
import _ from 'lodash'
export default {
  props: {
    placeholder: String,
    value: Object,
    label: String
  },
  mounted() {
    document.addEventListener('click', (e) => {
      this.isOpen = false
    }, false)
  },
  data() {
    return {
      isOpen: false,
      displayValue: '',
      labelValue: ''
    }
  },
  methods: {
    onArrow() {
      this.isOpen = !this.isOpen
    },
    onChange(item) {
      let obj = {
        id: item.id,
        displayValue: item.value,
        list: this.value.list
      }
      this.$emit('input', obj)
      this.$emit('onChange', obj)
    }
  },
  created() {
    this.labelValue = this.label ? this.label : ''

    let findItem = _.find(this.value.list, item => {
      return String(item.id) === String(this.value.id)
    })
    let displayValue = findItem ? findItem.value : ''

    this.$emit('input', {
      id: this.value.id,
      list: this.value.list,
      displayValue: displayValue
    })
  }
}
</script>


<style scoped>
.selct{
  height: 40px;
  display: inline-block;
  position: relative;
  cursor: pointer;
  user-select: none;
  outline: 0;
}
.select-inner{
  height: 40px;
  background-color: #fff;
  min-width: 282px;
  max-width: 700px;
  border:1px solid #ddd;
  display: flex;
  align-items: center;
}
.label{
  padding: 10px;
  padding-right: 0;
  color: #7f909c;
}
.title{
  padding-left: 10px;
  height: 40px;
  line-height: 40px;
  overflow: hidden;
  text-overflow:ellipsis;
  white-space: nowrap;
  flex-grow: 1;
}
.placeholder{
  color: #c2c2c2;
}
.arrow{
  flex-basis:40px;
  width: 40px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #ccc;
}

.select-items{
  position: absolute;
  width: 100%;
  margin: 0;
  padding: 0;
  border:1px solid #ddd;
  top: 39px;
  left: 0px;
  z-index: 100;
}

.select-list{
  max-height: 250px;
  overflow-y: auto;
  overflow-x: hidden;
  margin: 0;
  padding: 0;
}

.select-list li{
  background: #fff;
  padding-left: 19px;
  color: #3f495c;
  height: 40px;
  line-height: 40px;
  text-align: left;
  cursor: pointer;
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
  font-size: 14px;
  border-bottom: 1px solid #eee;
  box-sizing: border-box;
}
.select-list li:last-child{
  border:none;
}
.select-list li:hover{
  background: #efefef;
}

.rotate{
  transform-origin:center center;
  transform: rotate(-180deg);
  transition: transform .5s;
}

.rotate-back{
  transform-origin:center center;
  transform: rotate(0deg);
  transition: transform .5s;
}
</style>