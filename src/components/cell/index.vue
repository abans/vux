<template>
  <div class="weui_cell" :class="{'vux-tap-active': isLink}" @click="onClick">
    <div class="weui_cell_hd">
      <slot name="icon"></slot>
    </div>
    <div class="weui_cell_bd" :class="{'weui_cell_primary':primary==='title'}">
      <p>
        {{$t(title)}}
        <slot name="after-title"></slot>
      </p>
      <inline-desc v-if="inlineDesc">{{$t(inlineDesc)}}</inline-desc>
    </div>
    <div class="weui_cell_ft" :class="{'weui_cell_primary':primary==='content', 'with_arrow': isLink}">
      {{$t(value)}}
      <slot name="value"></slot>
      <slot></slot>
    </div>
  </div>
</template>

<script>
import InlineDesc from '../inline-desc'
import { go } from '../../libs/router'
let Afn

export default {
  components: {
    InlineDesc
  },
  props: {
    title: String,
    value: String,
    isLink: Boolean,
    inlineDesc: String,
    primary: {
      type: String,
      default: 'title'
    },
    link: {
      type: [String, Object]
    }
  },
  methods: {
    onClick () {
      if (Afn && Afn.window) {
        Afn.window.open(this.link, '', '_blank')
      } else {
        go(this.link, this.$router)
      }
    }
  }
}
</script>

<style lang="less">
@import '../../styles/tap.less';
@import '../../styles/weui/widget/weui_cell/weui_cell_global';

.weui_cell_ft.with_arrow:after {
  content: " ";
  display: inline-block;
  transform: rotate(45deg);
  height: 6px;
  width: 6px;
  border-width: 2px 2px 0 0;
  border-color: #C8C8CD;
  border-style: solid;
  position: relative;
  top: -1px;
  margin-left: .3em;
}
.weui_cell_bd p{
  font-size: 14px;
  color: #b5b5b5;
}
.weui_cell_bd p:only-child{
  font-size: 17px;
  color: #666;
}
.weui_cell_bd p+span{
  color: #666;
  font-size:17px;
}
</style>
