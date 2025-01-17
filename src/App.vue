<template>
  <div class="blog-app">
    <BaseLayout title="블로그 게시판">
       <!--게시글 작성 로딩 컴포넌트 호출  -->
     <PostForm
        :loading="loading" 
        @submit="createPost"
      />

     <LoadingSpinner v-if="loading"/>
     <ErrorMessage
        v-else-if="error"
        :message="error"
     />

     <PostList
     v-else
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
import LoadingSpinner from './components/common/LoadingSpinner.vue'
// import ErrorMessage from './components/common/ErrorMessage.vue'


//컴포넌트를 사용하려면 뭐부터 해야하지?
export default{
  components: {
    BaseLayout,
    PostList,
    PostForm,
    LoadingSpinner
  },

  data(){
    return{
      posts:[],
      loading: false,// 기본적으로는 loadingspinner가 돌아가지 않도록처리
      error:null
    }
  },
  methods: {
    async fetchPosts(){
      try{
        this.loading= true // 로딩 시작
       const response = await axios.get('https://jsonplaceholder.typicode.com/posts');
       this.posts = response.data 
       console.log(response.data);
      }catch(err){
        this.error = '게시물 로딩 실패'
      } finally{
        this.loading= false // 로딩 종료
      }

    },

    async createPost(newPost){
      // 현업에서는 db로 내용 저장 요청을 보냈는데 
      // 여기서는 db구축을 전혀 하지 않았기 때문에 
      // 일부러 저장했다 치고 결과를 로딩할수 있도록 처리.
      const response = await axios
      .post('https://jsonplaceholder.typicode.com/posts', newPost);
      this.posts.unshift(response.data) // 새 게시물을 목록 맨앞으로...
    },

    async editPost(updatePost){

      console.log(updatePost);
      const response 
      = await axios.put(
    `https://jsonplaceholder.typicode.com/posts/${updatePost.id}`, updatePost);
    
    // 수정된 게시물로 기존 게시물 교체
    const index = this.posts.findIndex(p=> p.id === updatePost.id);
    this.posts[index] = response.data
    },
    //게시물 삭제.
    // 1. deletePost 메서드를 완성시켜서 데이터 삭제를 구현해주세요
    // 2. LoadingSpinner 컴포넌트를 app에서 로딩시켜서
    //    기능이 정상적으로 작동하도록 코드를 완성.
    // 3. 예외처리를 추가하고 ErrorMessage 컴포넌트를 통해
    //    내용을 가져올수 있도록 처리.
    async deletePost(id){
      await axios.delete(`https://jsonplaceholder.typicode.com/posts/${id}`)
      this.posts = this.posts.filter(post => post.id !== id);
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