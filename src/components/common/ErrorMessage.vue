<template>
    <div class="error-message">
      <!-- 에러 메시지를 slot으로 커스터마이징 가능 -->
      <slot>
        {{ message }}  <!-- props로 전달받은 기본 메시지 -->
      </slot>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ErrorMessage',
    // props 정의
    props: {
      message: {
        type: String,
        required: true  // 필수 prop으로 지정
      }
    }
  }
  </script>
  
  <style scoped>
  .error-message {
    color: #dc3545; 
    padding: 10px;  
    background: #ffebee;
    border-radius: 4px;   
    margin: 10px 0;     
  }
  </style>
  