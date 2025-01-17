<template>

    <form class="post-form" @submit.prevent="handleSubmit">
        <!--값이 비어있으면 채워달라 알림메세지를 띄우는 속성 : required-->
        <BaseInput
            v-model="form.title"
            label="제목"
            :disabled="loading"
            required  
        />
        <BaseTextarea 
            v-model="form.body"
            label="내용"
            :disabled="loading"
            required
        />
        <BaseButton 
            type="submit"
            :loading="loading">게시글 작성하기</BaseButton>
    </form>
</template>

<script>
import BaseInput from './common/BaseInput.vue';
import BaseButton from './common/BaseButton.vue';
import BaseTextarea from './common/BaseTextarea.vue';

export default{
    components: {
      BaseInput,
      BaseTextarea,
      BaseButton
    },
    // props 정의
    props:{
        loading:{
            type:Boolean,
            default: false
        }
    },
    data(){
        return{
            form:{
                title: '',
                body: '',
                userId: 1 //임시 id값
            }
        }
    },
    methods: {
        handleSubmit(){
            this.$emit('submit', { ...this.form })
        }
    }
}
</script>

<style></style>