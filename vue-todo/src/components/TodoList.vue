<template>
  <div>
    <transition-group name="list" tag="ul">
      <!-- ul>li*3 -->
      <li v-for="(todoItem, index) in propsdata"  v-bind:key="todoItem.item" class="shadow">
        <!-- True면 {checkBtnCompleted}
        False면 아무것도 나타나지 않음 -->
        <em class="checkBtn fa-solid fa-check"
            v-bind:class="{checkBtnCompleted: todoItem.completed}"
            v-on:click="toggleComplete(todoItem, index)"
        ></em>
        <!-- 객체로 받아왔기 때문에 해당 속성을 불러오기 위해 .item -->
        <span v-bind:class="{textCompleted: todoItem.completed}"
              v-on:click="toggleComplete(todoItem, index)">
          {{ todoItem.item }}
        </span>
        <span class="removeBtn"
              v-on:click="removeTodo(todoItem, index)">
          <em class="fa-solid fa-trash-can"></em>
        </span>
      </li>
    </transition-group>
  </div>
</template>

<script>

export default {
  props: ['propsdata'],
  methods: {
    // removeTodo: function () {
    removeTodo: function (todoItem, index) {
      // 상위 컴포넌트로 실질적인 조작 기능이 올라갔기 때문에
      this.$emit('removeItem', todoItem, index);

    },
    toggleComplete: function (todoItem, index) {
      this.$emit('toggleItem', todoItem, index);
    }
  },

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
  align-self: center;
}

.checkBtnCompleted {
  color: #b3adad;
}

.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}

/* 리스트 아이템 트랜지션 효과 */
.list-enter-active, .list-leave-active {
  transition: all 1s;
}

.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */
{
  opacity: 0;
  transform: translateY(30px);
}

</style>