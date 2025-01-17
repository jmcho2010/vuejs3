<template>
    
</template>

<script>
import BaseButton from './common/BaseButton.vue'
import BaseInput from './common/BaseInput.vue'
import BaseTextarea from './common/BaseTextarea.vue'

export default{
    components: {
        BaseButton,
        BaseInput,
        BaseTextarea
    },
    props:{
        post:{
            type: Object,
            required: true
        }
    }
}

</script>

<style>
  .post-card {
    border: 1px solid #ddd;
    padding: 15px;
    margin-bottom: 10px;
    border-radius: 8px;
  }
  
  .post-content {
    margin: 10px 0;
  }
  
  .post-actions, .edit-actions {
    display: flex;
    gap: 10px;
    justify-content: flex-end;
  }
  
  .edit-form {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
</style>