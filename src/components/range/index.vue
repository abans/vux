<template>
  <div class="vux-range-input-box" style="position:relative;margin-right:30px;margin-left:50px;">
    <input class="vux-range-input" v-model="value" number>
    <input class="vux-range-input2" v-model="value2" number v-if="dual">
  </div>
</template>

<script>
const Powerange = require('./range/lib/powerange')

export default {
  props: {
    decimal: Boolean,
    value: {
      default: 0,
      type: Number
    },
    value2: {
      default: 0,
      type: Number
    },
    min: {
      type: Number,
      default: 0
    },
    minHTML: String,
    maxHTML: String,
    max: {
      type: Number,
      default: 100
    },
    dual: Boolean,
    step: {
      type: Number,
      default: 0
    },
    disabled: Boolean,
    disabledOpacity: {
      type: Number,
      default: 0.75
    },
    rangeBarHeight: {
      type: Number,
      default: 1
    },
    rangeHandleHeight: {
      type: Number,
      default: 30
    }
  },
  ready () {
    let options = {
      decimal: this.decimal,
      start: this.value,
      min: this.min,
      max: this.max,
      minHTML: this.minHTML,
      maxHTML: this.maxHTML,
      disable: this.disabled,
      disabledOpacity: this.disabledOpacity
    }
    if (this.step !== 0) {
      options.step = this.step
    }
    this.range = new Powerange(this.$el.querySelector('.vux-range-input'), options)
    if (this.dual) {
      this.range2 = new Powerange(this.$el.querySelector('.vux-range-input2'), options)
    }
    const handleTop = (this.rangeHandleHeight - this.rangeBarHeight) / 2
    this.$el.querySelector('.range-handle').style.top = `-${handleTop}px`
    this.$el.querySelector('.range-bar').style.height = `${this.rangeBarHeight}px`
  },
  watch: {
    value (val) {
      this.range.setStart(val)
    },
    value2 (val) {
      this.range2.setStart(val)
    }
  }
}
</script>

<style>
.range-bar{
  position: absolute;
}
.range-handle{
  z-index: 10;
  top: -13px!important;
}
.range-quantity {
  background-color: #a9acb1;
}
@import './powerange.css';
</style>

