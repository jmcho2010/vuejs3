<template>
    <button
      :type="type"         
      :class="['base-button', variant]" 
      :disabled="loading || disabled"     
      @click="$emit('click')"            
    >
      <!-- 로딩 스피너 -->
      <span v-if="loading" class="loading-spinner"></span>
      <slot></slot>  
    </button>
  </template>
  
  <script>
  export default {
    props: {
      type: {
        type: String,
        default: 'button'
      },
      variant: {
        type: String,
        default: 'primary',
        // 허용되는 variant 값 검증
        validator: value => ['primary', 'secondary', 'danger'].includes(value)
      },
      loading: {
        type: Boolean,
        default: false
      },
      disabled: {
        type: Boolean,
        default: false
      }
    }
  }
  </script>
  
  <style scoped>
  .base-button {
    padding: 8px 16px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-weight: 500;
    transition: all 0.3s ease;  
  }
  
  /* 버튼 변형 스타일 */
  .primary {
    background-color: #42b983;
    color: white;
  }
  
  .secondary {
    background-color: #606060;
    color: white;
  }
  
  .danger {
    background-color: #dc3545;
    color: white;
  }
  
  /* 로딩 스피너 애니메이션 */
  .loading-spinner {
    display: inline-block;
    width: 12px;
    height: 12px;
    border: 2px solid #fff;
    border-radius: 50%;
    border-top-color: transparent;
    animation: spin 1s linear infinite;
    margin-right: 8px;
  }
  
  @keyframes spin {
    to { transform: rotate(360deg); }
  }
  </style>
  