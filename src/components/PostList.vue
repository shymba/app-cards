<template>
  <div class="card" v-if="posts.length > 0">
    <transition-group name="post-list">
      <PostItem
          v-for="post in posts"
          :post="post"
          :key="post.id"
          @remove="$emit('remove', post)"
          @removeModal="$emit('removeModal', post)"
      />
    </transition-group>
  </div>
  <div v-else>
    <h3>Empty</h3>
  </div>
</template>

<script>
import PostItem from "@/components/PostItem";
export default {
  name: "PostList",
  components: {PostItem},
  props: {
    posts: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>
.card {
  max-width: 1200px;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  gap: 15px;
  justify-content: center;
}

.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.4s ease;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}

</style>