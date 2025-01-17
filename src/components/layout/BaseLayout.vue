<template>
    <div class="base-layout">
      <!-- 헤더 영역 -->
      <header class="header">
        <h1>{{ title }}</h1>  // props로 전달받은 제목
        <slot name="header"></slot>  // 헤더 영역 슬롯
      </header>
      
      <!-- 메인 컨텐츠 영역 -->
      <main class="main-content">
        <slot></slot>  // 기본 슬롯
      </main>
      
      <!-- 푸터 영역 -->
      <footer class="footer">
        <slot name="footer">
          <p>&copy; 2024 블로그 앱</p>  // 기본 푸터 내용
        </slot>
      </footer>
    </div>
</template>

<script>
    export default{

    }
</script>

<style></style>