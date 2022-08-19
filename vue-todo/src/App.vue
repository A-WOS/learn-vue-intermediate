<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput></TodoInput>
    <TodoList></TodoList>
    <TodoFooter></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

// var my_cmp = {
//   template: '<div>my component</div>'
// };

// new Vue({
//   el: '',
//   components: {
//     'my-cmp': my_cmp
//   }
// });

export default {
  components: {
    TodoHeader,
    TodoInput,
    TodoList,
    TodoFooter,
  }
}

</script>

<style scoped>
body {
  text-align: center;
  background-color: #F6F6F6;
}

input {
  border-style: groove;
  width: 200px;
}

button {
  border-style: groove;
}

/* 아래에 그림자 효과를 부여 */
.shadow {
  box-shadow: 5px 10px 10px rgba(0,0,0,0.03);
}
</style>