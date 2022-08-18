<template>
  <div>
    <!-- v-model: input에 입력된 
    테스트 값을 동적으로 뷰인스턴스 안에 매핑 -->
    <input type="text" v-model="newTodoItem">
    <button v-on:click="addTodo">add</button>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      newTodoItem: ""
    }
  },
  methods: {
    addTodo: function () {
      // console.log(this.newTodoItem);
      // 저장하는 로직
      localStorage.setItem(this.newTodoItem, this.newTodoItem);
      this.clearInput();
      
    },
    clearInput: function () {
      // 입력하고 add눌렀을시 input박스에 기존값을 비움
      this.newTodoItem = '';
    }
  }
}
</script>

<style>

</style>