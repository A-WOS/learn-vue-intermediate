<template>
  <div class="inputBox shadow">
    <!-- v-model: input에 입력된 
    테스트 값을 동적으로 뷰인스턴스 안에 매핑 -->
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <!-- <button v-on:click="addTodo">add</button> -->
    <span class="addContainer" v-on:click="addTodo">
      <em class="fa-solid fa-plus addBtn"></em>
    </span>
  </div>
</template>

<script>
import getDate from "../assets/commonJs/getDate";

export default {
  data: function () {
    return {
      newTodoItem: ""
    }
  },
  methods: {
    addTodo: function () {
      if (this.newTodoItem !== '') {
        // text가 체크되어있는지의 값, 텍스트값
        const obj = { completed: false, item: this.newTodoItem, time: getDate().date};
        // console.log(typeof obj.time); --> number
        // obj만 넣으면 안에 어떤값이 있는지를 모르기때문에 JSON.stringfiy작업을 해줘야됨
        // stringify 작업을 하면 Object를 Json문자열로 바꿔줌.
        // localStorage.setItem(this.newTodoItem, obj);
        localStorage.setItem(this.newTodoItem, JSON.stringify(obj));
        this.clearInput();
      }
    },
    clearInput: function () {
      // 입력하고 add눌렀을시 input박스에 기존값을 비움
      this.newTodoItem = '';
    }
  }
}
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  height: 40px;
  width: 80%;
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478FB, #8763FB);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  width: 50px;
  vertical-align: middle;
}
</style>