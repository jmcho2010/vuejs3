<template>
    <div class="post-list">
        <template v-if="posts.length">
            <PostCard 
                v-for="post in posts"
                :key="post.id"
                :post="post"
                @edit="$emit('edit', $event)"
                @delete="$emit('delete', $event)"
            />
        </template>
        <template v-else>
            <slot name="empty-message"></slot>
        </template>
    </div>
</template>

<script>
import PostCard from './PostCard.vue';

export default{
    components:{
        PostCard
    },
    props:{
        posts: {
            type: Array,
            required: true
        }
    },
    emits: ['edit', 'delete']
}
</script>

<style></style>