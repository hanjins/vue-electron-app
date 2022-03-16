<template>
  <div class="insertForm">
    <input
      ref="todoInput"
      v-model="todoInputMsg"
      type="text"
      class="inputField"
    >
    <button
      v-on:click="todoSave"
      type="button"
      class="ui-btn typePrimary"
    >
      <span>저장</span>
    </button>
  </div>
</template>

<script>
export default {
  name: 'TodoAdd',
  props: {
    setToday: String
  },
  data () {
    return {
      todoInputMsg: '',
      storageName: 'todoData',
      todoData : {
        todoId: null,
        todoMsg: '',
        todoComplete: false,
        todoRegDate: null
      }
    }
  },
  methods: {
    todoSave () {
      let getData = localStorage.getItem(this.storageName)
      let parseData = JSON.parse(getData);

      if(!this.todoInputMsg) {
        alert('할일을 입력하세요.')
        this.$refs.todoInput.focus()
      } else {
        // null(최초 or 새로고침) 이거나 기존 데이터가 없는 경우
        if(!getData) {
          parseData = []
          this.todoData.todoId = 1
        }
        // 기존 데이터가 있는 경우
        else {
          if(!this.todoId) {
            this.todoData.todoId = 1
          }

          parseData.forEach((el, idx, arr) => {
            if(idx === arr.length -1) { // 마지막 객체
              this.todoData.todoId = el.todoId + 1
            }
          });
        }

        this.todoData.todoMsg = this.todoInputMsg
        this.todoData.todoRegDate = this.setToday

        parseData.push(this.todoData)
        localStorage.setItem(this.storageName, JSON.stringify(parseData))

        this.todoInputMsg = ''
        this.$refs.todoInput.focus()
        
        this.$emit('key') // 부모 컴포넌트의 methods 사용
      }
    }
  }
}
</script>

<style scoped>
.insertForm {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  padding: 10px 10px 15px;
  background-color: #d9d9d9;
  border-top: 1px solid #b0b0b0;
  border-left: 1px solid #e0e0e0;
}
.insertForm:before {
  content: '';
  position: absolute;
  left: 0; top: 1px; z-index: -1;
  width: 100%; height: 100%;
  border-top: 2px solid #e0e0e0;
  border-left: 2px solid #e0e0e0;
}
.insertForm .inputField {
  display: block;
  width: calc(100% - 160px);
  height: 60px;
  padding: 0 15px;
  background-color: #f0f0f0;
  border: 1px solid #909090;
}
.insertForm .ui-btn {
  position: absolute;
  right: 10px;
  top: 10px;
  width: 150px;
  height: 60px;
  background-color: #c0c0c0;
  border: 1px solid #909090;
}
.insertForm .ui-btn:before {
  content: '';
  position: absolute;
  left: 0; top: 0;
  width: 100%; height: 100%;
  border-top: 2px solid #e0e0e0;
  border-left: 2px solid #e0e0e0;
}
</style>
