<template>
  <div class="blog-app">
    <BaseLayout title="블로그 게시판">
       <!--게시글 작성 로딩 컴포넌트 호출-->
      <PostForm 
        
      />
     


   <!--로딩 아이콘과 에러메세지 컴포넌트 호출
           조건에 맞게 로딩할 필요가 있음.-->
      <!-- <LoadingSpinner />
      <ErrorMessage />
      <PostList>
        <template #empty-message>
          <p>게시물이 없습니다.</p>
        </template>
      </PostList> -->
    </BaseLayout>
  </div>

</template>

<script>
import axios from 'axios'
//import PostForm from './components/PostForm.vue'
// import BaseLayout from './components/layouts/BaseLayout.vue'
// import PostList from './components/PostList.vue'
// import PostCard from './components/PostCard.vue'
// import LoadingSpinner from './components/common/LoadingSpinner.vue'
// import ErrorMessage from './components/common/ErrorMessage.vue'
// import BaseButton from './components/common/BaseButton.vue'
// import BaseInput from './components/common/BaseInput.vue'
// import BaseTextarea from './components/common/BaseTextarea.vue'

//컴포넌트를 사용하려면 뭐부터 해야하지?
export default{
  // components: {
  //   PostForm
  // },

  data(){
    return{
      posts:[]
    }
  },
  methods: {
    created(){
      // 굳이 데이터 로딩 구조를 분리한 이유는
      // 첫 로딩시 데이터 뿐만이 아니라 추후 다른 기능들을 로딩할 가능성도 있어서
      // 재사용성과 확장성을 위해 분리.
      this.fetchPosts();
    },
    async fetchPosts(){
       const response = await axios.get('https://jsonplaceholder.typicode.com/posts') 
       console.log(response.data);
    }
  }
}


</script>

<style scoped>
</style>