<template>
  <div class="blog-app">
    <BaseLayout title="블로그 게시판">
       <!--게시글 작성 로딩 컴포넌트 호출  -->
     <PostForm
        :loading="loading" 
        @submit="createPost"
      />
    <!-- 
     <LoadingSpinner v-if="loading"/>
     <ErrorMessage
        v-else-if="error"
        :message="error"
     /> -->

     <PostList
      :posts="posts"
      @edit="editPost"
      @delete="deletePost"
      >
        <template #empty-message>
          <p>게시물이 없습니다.</p>
        </template>
      </PostList>
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
import PostForm from './components/PostForm.vue'
import BaseLayout from './components/layout/BaseLayout.vue'
import PostList from './components/PostList.vue'
// import LoadingSpinner from './components/common/LoadingSpinner.vue'
// import ErrorMessage from './components/common/ErrorMessage.vue'


//컴포넌트를 사용하려면 뭐부터 해야하지?
export default{
  components: {
    BaseLayout,
    PostList,
    PostForm
  },

  data(){
    return{
      posts:[],
      loading: false,
      error:null
    }
  },
  methods: {
    async fetchPosts(){
       const response = await axios.get('https://jsonplaceholder.typicode.com/posts');
       this.posts = response.data 
       console.log(response.data);
    },

    async createPost(newPost){
      // 현업에서는 db로 내용 저장 요청을 보냈는데 
      // 여기서는 db구축을 전혀 하지 않았기 때문에 
      // 일부러 저장했다 치고 결과를 로딩할수 있도록 처리.
      const response = await axios
      .post('https://jsonplaceholder.typicode.com/posts', newPost);
      this.posts.unshift(response.data) // 새 게시물을 목록 맨앞으로...
    }
  },
  created(){
      // 굳이 데이터 로딩 구조를 분리한 이유는
      // 첫 로딩시 데이터 뿐만이 아니라 추후 다른 기능들을 로딩할 가능성도 있어서
      // 재사용성과 확장성을 위해 분리.
      alert("test");
      this.fetchPosts();
  }
}


</script>

<style scoped>
</style>