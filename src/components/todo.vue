<template>
  <!-- 最外层容器 -->
  <div class="page lists-show">
    <nav>
      <!-- 移动端左侧导航图标 -->
      <div class="nav-group">
        <a class="nav-item">
          <span class="icon-list-unordered"></span>
        </a>
      </div>
      <h1 class="title-page">
        <!-- 标题 -->
        <span class="title-wrapper">{{todo.title}}</span>
        <!-- 数量 -->
        <span class="count-list">{{todo.count}}</span>
      </h1>
      <!-- 右侧删除，锁定图标容器 -->
      <div class="nav-group right">
        <div class="options-web">
          <a class="nav-item">
            <!-- 锁定图标 -->
            <span class="icon-lock" v-if="todo.locked"></span>
            <span class="icon-unlock" v-else></span>
          </a>
          <a class="nav-item">
            <!-- 删除图标 -->
            <span class="icon-trash"></span>
          </a>
        </div>
      </div>
      <!-- 新增单个代办单项输入框,监听了回车事件，双向绑定text值,监听了disabled属性，在todo.locked为true的情况下无法编辑 -->
      <div class="form todo-new input-symbol">
        <input type="text" v-model="text" placeholder="请输入" @keyup.enter="onAdd" :disabled="todo.locked">
        <span class="icon-add" @click="onAdd"></span>
      </div>
    </nav>
    <!-- 容器下半部分 -->
    <div class="content-scrollable list-items">
      <!-- 这里v-for会循环我们在data函数事先定义好的items模拟数据，循环后拿到单个对象，在通过prop把数据传输给子组件item -->
      <div v-for="item in items">
        <item :item="item"></item>
      </div>
    </div>
  </div>
</template>
<script>
// 导入item组件
import item from './item.vue'
  export default {
    components: {
      item
    },
    data() {
      return {
        todo: {
          title: '星期一',
          count: 12,
          locked: false
        },
        items: [{
            checked: false,
            text: '新的一天',
            isDelete: false
          },
          {
            checked: false,
            text: '新的一天',
            isDelete: false
          },
          {
            checked: false,
            text: '新的一天',
            isDelete: false
          }
        ],
        text: ''
      }
    },
    methods: {
      onAdd() {
        this.items.push({
          checked: false,
          text: this.text,
          isDelete: false
        })
        this.text = ""
      }
    }
  }

</script>
<style lang="less">
  @import '../common/style/nav.less';
  @import '../common/style/form.less';
  @import '../common/style/todo.less';

</style>
