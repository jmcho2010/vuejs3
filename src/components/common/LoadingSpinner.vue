<template>
    <div class="loading-container">
      <!-- 로딩 스피너 시각적 요소 -->
      <div class="loading-spinner"></div>
      <!-- 기본 텍스트를 제공하되, 커스텀 가능하도록 slot 사용 -->
      <slot>로딩 중...</slot>
    </div>
  </template>

  <style scoped>
  /* 로딩 컨테이너 스타일링 */
  .loading-container {
    text-align: center;  
    padding: 20px;      
  }
  
  /* 스피너 애니메이션 스타일링 */
  .loading-spinner {
    display: inline-block;
    width: 40px;        
    height: 40px;
    border: 4px solid #f3f3f3;  
    border-top: 4px solid #42b983;  
    border-radius: 50%;  
    animation: spin 1s linear infinite;  
  }
  
  /* 회전 애니메이션 정의 */
  @keyframes spin {
    to { transform: rotate(360deg); } 
  }
  </style>
  