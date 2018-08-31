<template>
  <!-- 菜单容器 -->
  <div class="list-todos">
    <!-- 单个菜单容器 -->
    <a  class="list-todo activeListClass list" v-for="item in items">
      <!-- 锁图标 -->
      <span class="icon-lock" v-if="item.locked"></span>
      <!-- 数字 -->
      <span class="count-list" v-if="item.count > 0">{{ item.count }}</span>
      {{ item.title }}
    </a>
    <!-- 新增菜单 -->
    <a class="link-list-new">
      <span class="icon-plus"></span>
      新增
    </a>
  </div>
</template>
<script>
export default {
  data() {
    return {
      items: [{
        id: 1,
        title: '星期一',
        count: 1,
        locked: true
      }, {
        id: 2,
        title: '星期二',
        count: 2,
        locked: true
      }, {
        id: 3,
        title: '星期三',
        count: 3,
        locked: false
      }]
    }
  }
}
</script>

<style lang="less">
  @import '../common/style/menu.less';

</style>
