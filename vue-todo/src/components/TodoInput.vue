<template>
  <div class="inputBox shadow">
    <!-- v-model: input에 입력된 
    테스트 값을 동적으로 뷰인스턴스 안에 매핑 -->
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <!-- <button v-on:click="addTodo">add</button> -->
    <span class="addContainer" v-on:click="addTodo">
      <em class="fa-solid fa-plus addBtn"></em>
    </span>

    <Modal v-if="showModal" @close="showModal = false">
      <!--
    you can use custom content here to overwrite
    default content
    -->
      <h3 slot="header">
        경고!
      </h3>

      <!-- 과제 -->
      <!-- 바디 : 무언가를 입력하세요. -->
      <h3 slot="body">
        무언가를 입력하세요.
      </h3>
      <!-- 푸터 : copy right -->
      <h3 slot="footer">
        copy right
      </h3>
    </Modal>

  </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
  data: function () {
    return {
      newTodoItem: "",
      showModal: false
    }
  },
  methods: {
    addTodo: function () {
      if (this.newTodoItem !== '') {
        /* 입력되는 부분들이 상위 컴포넌트로 이동했기 때문에
        상위 컴포넌트로 값만 보내주면됨 */
        // this.$emit('이벤트 이름', 인자1, 인자2, ...);
        this.$emit('addTodoItem', this.newTodoItem);
        this.clearInput();
      } else {
        // 입력값이 없으면 예외처리로 경고창
        // alert('type sth');
        this.showModal = !this.showModal;

      }
    },
    clearInput: function () {
      // 입력하고 add눌렀을시 input박스에 기존값을 비움
      this.newTodoItem = '';
    }
  },
  components: {
    Modal: Modal
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