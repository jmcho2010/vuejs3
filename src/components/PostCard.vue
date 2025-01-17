<template>
    <div class="post-card">
        <!-- 수정모드와 아닐 때를 구분-->
        <div v-if="isEditing" class="edit-form">
            <BaseInput 
                v-model="editiedPost.title"
                label="제목"
                placeholder="제목을 입력하세요."
            />
            <BaseTextarea
                v-model="editiedPost.body"
                label="내용"
                placeholder="내용을 입력하세요"
            />
            <div class="edit-actions">
                <BaseButton @click="saveEdit">저장</BaseButton>
                <BaseButton variant="secondary" @click="cancelEdit">취소</BaseButton>
            </div>
        </div>
        <!-- 수정모드가 아닌 일반모드일시 -->
        <div v-else>
            <h3>{{ post.title }}</h3>
            <div class="post-content">
                <p>{{ post.body }}</p>
            </div>
            <div class="post-actions">
                <BaseButton variant="secondary" @click="startEdit">수정</BaseButton>
                <BaseButton variant="danger" @click="$emit('delete', post.id)">삭제</BaseButton>
            </div>
        </div>
    </div>
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
    }, 
    data(){
        return{
            isEditing:false, // 수정모드의 구분을 위한 데이터
            editiedPost:{  // 수정모드로 접근시 타이틀과 바디를 초기화
                title: '',
                body: ''
            }
        }
    },
    methods:{
        startEdit(){
            this.isEditing = true;
            // 꼭 스프레드로 써야하는가?
            // 1. 객체의 무결성 유지
            // 2. 객체를 직접 전달할때는 예기치않은 부작용이 발생할수 있음.
            // 3. Vue의 반응 시스템 자체를 더 효율적으로 작동시킬수 있음.
            this.editiedPost = { ...this.post }
        },
        saveEdit(){
            this.$emit('edit', this.editiedPost)
            this.isEditing = false
        },
        cancelEdit(){   
            this.isEditing = false
            this.editiedPost = { ...this.post }
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