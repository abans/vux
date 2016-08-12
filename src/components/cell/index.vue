<template>
  <div class="weui_cell" :class="{'vux-tap-active': isLink}" @click="onClick">
    <div class="weui_cell_hd">
      <slot name="icon"></slot>
    </div>
    <div class="weui_cell_bd" :class="{'weui_cell_primary':primary==='title'}">
      <p>
        <slot name="before-title"></slot>
        {{$t(title)}}
        <slot name="after-title"></slot>
      </p>
      <inline-desc v-if="inlineDesc">{{$t(inlineDesc)}}</inline-desc>
    </div>
    <div class="weui_cell_ft nowrap-word" :class="{'weui_cell_primary':primary==='content'}">
      {{$t(value)}}
      <slot name="value"></slot>
      <slot></slot>
    </div>
    <div class="weui_cell_ft" :class="{'with_arrow': isLink}">
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

.nowrap-word {
  padding-left:10px;
  text-overflow:ellipsis;
  white-space:nowrap;
  overflow:hidden;
}
.weui_cell_ft.with_arrow:after {
  content: " ";
  display: inline-block;
  transform: rotate(45deg);
  height: 12px;
  width: 12px;
  border-width: 1px 1px 0 0;
  border-color: #C8C8CD;
  border-style: solid;
  position: relative;
  top: 0;
  right: 3px;
  margin-left: .3em;
}
</style>
