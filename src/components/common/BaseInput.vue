<template>
    <div class="base-input">
      <!-- label이 있는 경우에만 표시 -->
      <label v-if="label" :for="id" class="input-label">
        {{ label }}
        <span v-if="required" class="required">*</span>
      </label>
      
      <input
        :id="id"
        :type="type"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
        :placeholder="placeholder"
        :disabled="disabled"
        :required="required"
        class="input-field"
        v-bind="$attrs"
      >
      
      <!-- 에러 메시지가 있는 경우 표시 -->
      <span v-if="error" class="error-message">
        {{ error }}
      </span>
    </div>
  </template>
  
  <script>
  export default {
    name: 'BaseInput',
    props: {
      modelValue: {
        type: [String, Number],
        default: ''
      },
      label: {
        type: String,
        default: ''
      },
      type: {
        type: String,
        default: 'text'
      },
      placeholder: {
        type: String,
        default: ''
      },
      required: {
        type: Boolean,
        default: false
      },
      disabled: {
        type: Boolean,
        default: false
      },
      error: {
        type: String,
        default: ''
      },
      id: {
        type: String,
        default() {
          return `input-${Math.random().toString(36).substr(2, 9)}`
        }
      }
    },
    emits: ['update:modelValue']
  }
  </script>
  
  <style scoped>
  .base-input {
    display: flex;
    flex-direction: column;
    margin-bottom: 1rem;
  }
  
  .input-label {
    margin-bottom: 0.5rem;
    font-weight: 500;
    color: #2c3e50;
  }
  
  .required {
    color: #dc3545;
    margin-left: 4px;
  }
  
  .input-field {
    padding: 0.5rem;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-size: 1rem;
    transition: border-color 0.3s ease;
  }
  
  .input-field:focus {
    outline: none;
    border-color: #42b983;
    box-shadow: 0 0 0 2px rgba(66, 185, 131, 0.1);
  }
  
  .input-field:disabled {
    background-color: #f5f5f5;
    cursor: not-allowed;
  }
  
  .error-message {
    color: #dc3545;
    font-size: 0.875rem;
    margin-top: 0.25rem;
  }
  </style>
  