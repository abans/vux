<template>
  <div class="vux-checker-item" :class="classNames" @click="select">
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: [String, Number, Boolean],
      required: true
    },
    disabled: Boolean
  },
  computed: {
    classNames () {
      const names = {
        'vux-tap-active': !this.disabled
      }
      if (this.$parent.defaultItemClass) {
        names[this.$parent.defaultItemClass] = true
      }
      if (this.$parent.selectedItemClass) {
        if (this.$parent.type === 'radio') {
          names[this.$parent.selectedItemClass] = this.$parent.value === this.value
        } else {
          if (this.$parent.value.indexOf) {
            names[this.$parent.selectedItemClass] = this.$parent.value.indexOf(this.value) > -1
          } else {
            names[this.$parent.selectedItemClass] = this.$parent.value
          }
        }
      }
      if (this.$parent.disabledItemClass) {
        names[this.$parent.disabledItemClass] = this.disabled
      }
      return names
    }
  },
  methods: {
    select () {
      if (this.$parent.type === 'radio') {
        this.selectRadio()
      } else {
        this.selectCheckbox()
      }
    },
    selectRadio () {
      if (!this.disabled) {
        this.$parent.$set('value', this.value)
        this.$emit('on-item-click', this.value, this.disabled)
      }
    },
    selectCheckbox () {
      if (!this.disabled) {
        if (this.$parent.value.indexOf) {
          const index = this.$parent.value.indexOf(this.value)
          if (index > -1) {
            this.$parent.value.splice(index, 1)
          } else {
            if (!this.$parent.max || (this.$parent.max && this.$parent.value.length < this.$parent.max)) {
              this.$parent.value.push(this.value)
            }
          }
        } else {
          if (this.$parent.value) {
            this.$parent.$set('value', false)
          } else {
            this.$parent.$set('value', true)
          }
        }
        this.$emit('on-item-click', this.value, this.disabled)
      }
    }
  }
}
</script>

<style lang="less">
@import '../../styles/tap.less';
</style>
