<template>
  <!-- 最外层容器 -->
  <section class="container">
    <!-- 左侧容器 -->
    <section class="menu">
      <menus></menus>
    </section>
    <!-- 右侧容器 -->
    <section class="content-container">
        <todo></todo>
    </section>
  </section>
</template>
<script>
// 导入menus组件
import menus from './menus.vue'
// 导入todo组件
import todo from './todo.vue'
export default {
  components: {
    // 注册menus组件，让其可在template调用
    menus,
    todo
  }
}

</script>

<style lang="less">
  @import '../common/style/layouts.less';

</style>
