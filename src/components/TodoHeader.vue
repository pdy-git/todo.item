<template>
  <header class="header">
    <h1>todos</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox" />
    <label for="toggle-all"></label>
    <!-- label 可以关联一个表单标签 -->
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      @keyup.enter="enterFn"
      v-model="task"
    />
  </header>
</template>

<script>
export default {
  data() {
    return {
      task: "",
    };
  },
  methods: {
    enterFn() {
      //  非空校验
      if (this.task.trim == "") {
        return alert("内容不能为空");
      }
      //数据添加
      this.$emit("add", this.task);
    },
  },
};
</script>
