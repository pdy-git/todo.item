<template>
  <section class="todoapp">
    <!-- 除了驼峰, 还可以使用-转换链接 -->
    <TodoHeader @add="addFn"></TodoHeader>
    <TodoMain :list="showList" @del="delFn"></TodoMain>
    <TodoFooter :count="count" @changeType="typeFn"></TodoFooter>
  </section>
</template>

<script>
// 1.0 样式引入
import "./assets/style/base.css";
import "./assets/style/index.css";

import TodoHeader from "./components/TodoHeader.vue";
import TodoMain from "./components/TodoMain.vue";
import TodoFooter from "./components/TodoFooter.vue";

export default {
  data() {
    return {
      list: [
        { id: 100, name: "吃饭", isDone: true },
        { id: 102, name: "睡觉", isDone: false },
        { id: 103, name: "打豆豆", isDone: true },
      ],
      getSel: "",
    };
  },
  computed: {
    count() {
      //ele.isDone == false
      return this.list.filter((ele) => !ele.isDone).length;
    },
    showList() {
      if (this.getSel == "no") {
        return this.list.filter((ele) => !ele.isDone);
      } else if (this.getSel == "yes") {
        return this.list.filter((ele) => ele.isDone === true);
      } else {
        return this.list;
      }
    },
  },
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  methods: {
    addFn(val) {
      // console.log(val);
      this.list.push({
        name: val,
        isDone: false,
        // id: this.list[this.list.length-1].id + 1
        id:
          (this.list.length > 0 && this.list[this.list.length - 1].id + 1) ||
          100,
      });
    },
    delFn(id) {
      const index = this.list.findIndex((ele) => ele.id == id);
      this.list.splice(index, 1);
    },
    typeFn(str) {
      //all no yes
      this.getSel = str;
    },
  },
};
</script>
