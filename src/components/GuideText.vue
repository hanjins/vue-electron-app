<template>
  <div>
    <ul class="ui-list">
      <li>오늘의 할일을 입력하세요.</li>
      <li>등록된 할일은 기본적으로 오늘이 지나면 삭제됩니다.</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'GUideText'
}
</script>

<style scoped>
.ui-list {
  padding: 10px 20px;
  border: 1px solid #999;
  background-color: #e0e0e0;
}
.ui-list li {
  position: relative;
  padding-left: 20px;
  font-size: 14px;
}
.ui-list li:before {
  content: 'ㆍ';
  position: absolute;
  left: 0;
  margin-right: 5px;
}
</style>
