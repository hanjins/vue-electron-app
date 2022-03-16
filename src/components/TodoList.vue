<template>
  <div>
    <div class="todoList">
      <p class="noData" v-if="!resultBoolean">등록된 TODO 없음</p>
      <ul class="todoItem" v-if="resultBoolean">
        <li
          v-for="todoData in todoDatas"
          v-bind:key="todoData.todoId"
          v-bind:class="{ completed: todoData.todoComplete }"
        >
          <span>{{ todoData.todoMsg }}</span>
          <todoControl
            v-bind:todoId="todoData.todoId"
            v-on:keyComplete="todoComplete"
            v-on:keyDelete="todoDelete"
          />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import todoControl from './TodoControl'
export default {
  name: 'TodoList',
  components: {
    todoControl
  },
  props: {
    setToday: String
  },
  data () {
    return {
      resultBoolean: false,
      storageName: 'todoData',
      resultData: null,
      todoDatas: []
    }
  },
  created () {
    this.printList()
  },
  methods: {
    printList () {
      this.resultData = JSON.parse(localStorage.getItem(this.storageName))

      if(!this.resultData || this.resultData.length === 0) { // 데이터 유무에 따른 디스플레이 변환
        this.resultBoolean = false
      } else {
        this.resultBoolean = true
        this.todoDatas = this.resultData

        // 오늘 이전 데이터 삭제
        this.resultData.forEach((el) => {
          if(el.todoRegDate < this.setToday) {
            this.todoDelete(el.todoId)
          }
        })
      }
    },
    todoComplete (n) {
      // 선택한 항목의 todoComplete 을 true 로 변경
      this.resultData.forEach((el, idx, arr) => {
        if(n == el.todoId) {
          el.todoComplete = true

          // 데이터 저장
          localStorage.setItem(this.storageName, JSON.stringify(arr))

        }
      })
    },
    todoDelete (n) {
      this.resultData.forEach((el, idx, arr) => {
        if(n === el.todoId) {

          // this.resultData 중에 해당 데이터를 삭제
          // array.splice(start, deleteCount, items)
          this.resultData.splice(idx, 1)

          // 데이터 저장
          localStorage.setItem(this.storageName, JSON.stringify(arr))
        }
      })
    }
  }
}
</script>

<style scoped>
.todoList {
  height: 410px;
  padding: 20px;
  overflow: auto;
}
.todoList .noData {
  padding: 50px 0;
  text-align: center;
}
.todoList .todoItem > li {
  position: relative;
  padding: 20px 150px 20px 20px;
  border: 1px solid transparent;
}
.todoList .todoItem > li:hover {
  border-color: #d0d0d0;
  border-radius: 7px;
  box-shadow: 0 0 10px rgba(0,0,0,0.2);
}
.todoList .todoItem > li.completed > span {
  color: #999;
  font-style: italic;
  text-decoration: line-through;
}
</style>
