<template>
  <div id="app">
    <TodoHeader></TodoHeader>
<!--    <TodoInput v-on=하위 컴포넌트에서 발생시킨 이벤트 이름 = "현재 컴포넌트의 메서드 명"></TodoInput>-->
    <TodoInput v-on:addTodoItem="addOneItem"></TodoInput>
    <!--    <TodoList v-bind:내려보낼 프롭스 속성 이름 = "현재 위치의 컴포넌트 이름"></TodoList>-->
    <TodoList v-bind:propsdata="todoItems"
              v-on:removeItem="removeOneItem"
              v-on:toggleItem="toggleOneItem"
    ></TodoList>
    <TodoFooter v-on:clearAll="clearAllItems"></TodoFooter>
  </div>
</template>

<script>
// 등록된 순으로 정렬하기 위하여 import
import getDate from "@/assets/commonJs/getDate";

import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  // TodoList.vue 에서 App.vue 로 이동
  data() {
    return {
      todoItems: []
    }
  },
  methods: {
    addOneItem(todoItem){
      // TodoInput 에 있었을 때는 this.newTodoItem 이 유효하기 때문에 인자를 받아서 해줘야됌
      const obj = { completed: false, item: todoItem, time: getDate().date};
      // 로컬 스토리지의 목록과 화면에 있는 파일 목록이 동기화 됨.
      localStorage.setItem(todoItem, JSON.stringify(obj));
      this.todoItems.push(obj);
    },
    removeOneItem(todoItem, index){
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1);
    },
    toggleOneItem(todoItem, index){
      // propsdata 를 TodoList.vue 로 내리고 toggleComplete 에서 다시 올려서 받아오기 때문에
      // 좋지 않은 코드다. 따라서 App.vue 에서 todoItems 에서 바로 받아오기 위해 코드를 수정한다.
      // todoItem.completed = !todoItem.completed;
      // console.log(this.todoItems[index].completed);
      this.todoItems[index].completed = !this.todoItems[index].completed;
      // 로컬 스토리지의 데이터를 갱신
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    clearAllItems(){
      // 모든 데이터가 삭제
      localStorage.clear();
      // 로컬 스토리지만 비우고 배열은 비우지 않았기 때문에 코드 추가
      this.todoItems = [];
    }
  },
  // TodoList.vue 에서 App.vue 로 이동
  // created() { // same code
  created: function () {
    if (localStorage.length > 0) {
      // var 대신 let, const 사용 - 호이스팅 관련
      for (let i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
        }
      }
    }
  },
  components: {
    TodoHeader,
    TodoInput,
    TodoList,
    TodoFooter,
  }
}

</script>

<style>
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
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>