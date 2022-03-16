<template>
  <div>
    <button type="button" class="ui-btn typePrimary" v-on:click="todoComplete"><span>완료</span></button>
    <button type="button" class="ui-btn typeError" v-on:click="todoDelete"><span>삭제</span></button>
  </div>
</template>

<script>
export default {
  name: 'todoControl',
  props: {
    todoId: Number
  },
  methods: {
    todoComplete () {
      this.$emit('keyComplete', this.todoId)
    },
    todoDelete () {
      this.$emit('keyDelete', this.todoId);
    }
  }
}
</script>

<style scoped>
.hidden { position:absolute !important; width:0 !important; height:0 !important; z-index:-1 !important; color:transparent !important; overflow:hidden !important; font-size:xx-small !important; line-height:0 !important; min-height:0 !important; max-height:0 !important; }
.todoList .todoItem > li:hover .ui-btn { display: block; }
.ui-btn {
  display: none;
  position: absolute;
  top: 50%;
  margin-top: -16px;
  padding: 3px 10px;
  color: #fff;
  font-size: 14px;
  border: 1px solid transparent;
  border-radius: 3px;
}
.ui-btn.typePrimary {
  right: 78px;
  margin-top: -16px;
  background-color: green;
  border-color: green;
}
.completed .ui-btn.typePrimary {
  display: none !important;
}
.ui-btn.typeError {
  right: 25px;
  background-color: red;
  border-color: red;
}
</style>
