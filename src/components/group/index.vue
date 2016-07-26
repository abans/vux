<template>
  <div>
    <div class="weui_group_title" v-if="title">
      <div class="weui_cells_title weui_cell_bd" :class="{'weui_cell_primary':primary==='title'}">
        <p>{{$t(title)}}</p>
      </div>
      <div class="weui_cells_title weui_cell_ft" :class="{'weui_cell_primary':primary==='content'}">
      {{$t(value)}}<slot name="value"></slot>
      </div>
    </div>
    <div class="weui_cells" :class="{'vux-group-title':title}">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import GroupTitle from '../group-title'

export default {
  components: {
    GroupTitle
  },
  props: {
    title: String,
    value: String,
    primary: {
      type: String,
      default: 'title'
    },
    titleColor: String
  }
}
</script>

<style lang="less">
@import '../../styles/weui/widget/weui_cell/weui_access';
@import '../../styles/weui/widget/weui_cell/weui_cell_global';

.vux-no-group-title {
  margin-top:15px;
}
.vux-group-title {
  margin-top:0!important;
}
.weui_cells > a {
  color:#000;
}
div.weui_cells_title{
  padding-right:0;
}
.weui_group_title .weui_cells_title p{
  font-size: 14px;
  color: #888;
}
.weui_group_title {
  position: relative;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
}
</style>
