<template>
    <div class="base-textarea">
      <label v-if="label" :for="id" class="textarea-label">
        {{ label }}
        <span v-if="required" class="required">*</span>
      </label>
      
      <textarea
        :id="id"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
        :placeholder="placeholder"
        :disabled="disabled"
        :required="required"
        :rows="rows"
        class="textarea-field"
        v-bind="$attrs"
      ></textarea>
      
      <span v-if="error" class="error-message">
        {{ error }}
      </span>
    </div>
  </template>
  
  <script>
  export default {
    name: 'BaseTextarea',
    props: {
      modelValue: {
        type: String,
        default: ''
      },
      label: {
        type: String,
        default: ''
      },
      placeholder: {
        type: String,
        default: ''
      },
      rows: {
        type: Number,
        default: 4
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
          return `textarea-${Math.random().toString(36).substr(2, 9)}`
        }
      }
    },
    emits: ['update:modelValue']
  }
  </script>
  
  <style scoped>
  .base-textarea {
    display: flex;
    flex-direction: column;
    margin-bottom: 1rem;
  }
  
  .textarea-label {
    margin-bottom: 0.5rem;
    font-weight: 500;
    color: #2c3e50;
  }
  
  .required {
    color: #dc3545;
    margin-left: 4px;
  }
  
  .textarea-field {
    padding: 0.5rem;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-size: 1rem;
    font-family: inherit;
    resize: vertical;
    min-height: 100px;
    transition: border-color 0.3s ease;
  }
  
  .textarea-field:focus {
    outline: none;
    border-color: #42b983;
    box-shadow: 0 0 0 2px rgba(66, 185, 131, 0.1);
  }
  
  .textarea-field:disabled {
    background-color: #f5f5f5;
    cursor: not-allowed;
  }
  
  .error-message {
    color: #dc3545;
    font-size: 0.875rem;
    margin-top: 0.25rem;
  }
  </style>
  