<template>
  <!-- 菜单容器 -->
  <div class="list-todos">
    <!-- 单个菜单容器 -->
    <a class="list-todo activeListClass list" :class="{'active': item.id === todoId}" v-for="item in items" @click="goList(item.id)">
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
  // 引入封装好的两个接口函数
  import {
    getTodoList,
    addTodo
  } from '../api/api';
  export default {
    data() {
      return {
        //   items: [{
        //     id: 1,
        //     title: '星期一',
        //     count: 1,
        //     locked: true
        //   }, {
        //     id: 2,
        //     title: '星期二',
        //     count: 2,
        //     locked: true
        //   }, {
        //     id: 3,
        //     title: '星期三',
        //     count: 3,
        //     locked: false
        //   }]
        items: [],
        todoId: ''
      }
    },
    created() {
      // 调用请求菜单列表数据的接口
      getTodoList({}).then(res => {
        const TODOS = res.data.todos; // 数据都会返回在res.data里面。
        this.items = TODOS; // 我的把菜单数据赋值给定义的this.items
        this.todoId = TODOS[0].id; // 把菜单数据的默认的第一个对象的id赋值给默认选中的id
      })
    },
    methods: {
      goList(id) { // 点击菜单时候,替换选中id
        this.todoId = id;
      },
      addTodoList() { // 点击新增按钮时候
        // 调用新增菜单的接口，在接口调用成功在请求数据
        addTodo({}).then(data => {
          getTodoList({}).then(res => {
            const TODOS = res.data.todos;
            this.todoId = TODOS[TODOS.length - 1].id;
            this.items = TODOS;
          });
        });
      }
    }
  }

</script>

<style lang="less">
  @import '../common/style/menu.less';

</style>
