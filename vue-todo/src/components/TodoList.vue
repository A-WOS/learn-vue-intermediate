<template>
  <div>
    <!-- ul>li*3 -->
    <ul>
      <!-- <li v-for="todoItem in todoItems" v-bind:key="todoItem" class="shadow"> -->
      <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem" class="shadow">
        {{ todoItem }}
        <!-- <span class="removeBtn" v-on:click="removeTodo"> -->
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
          <i class="fa-solid fa-trash-can"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      todoItems: []
    }
  },  
  methods: {
    // removeTodo: function () {
    removeTodo: function(todoItem, index) {
      // console.log('remove items');
      console.log(todoItem, index);
      // 로컬 스토리지(db)와 스크립트(html)창은 독립적이기에
      // 실시간으로 삭제되는것을 보고 싶다면 LocalStorage에서 지워주고
      // script에서 splice로 해당 index를 1만큼 제거하면 됨.
      // splice - 배열의 기존 요소를 삭제 또는 교체하거나 새 요소를 추가하여 
      //          배열의 내용을 변경
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index, 1);
    }
  },
  created: function () {
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
          this.todoItems.push(localStorage.key(i));
        }
        // console.log(localStorage.key(i));
      }
    }
  }
}
</script>

<style scoped>


ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}

li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}

.removeBtn {
  margin-left: auto;
  color: #de4343;
}

.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}

.checkBtnComplated {
  color: #b3adad;
}

.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}


</style>