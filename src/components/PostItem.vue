<template>
  <div class="post">
    <div>
      <div><strong>ID:</strong>{{post.id}}</div>
      <div><strong>Title:</strong>{{post.title}}</div>
      <div><strong>Description:</strong>{{post.body}}</div>
    </div>
    <div class="post__btns">
      <MyBtn
          @click="$emit('remove', post)"
          style="margin-left: 0"
      >
        Delete
      </MyBtn>
      <MyBtn @click="showModal">
        Modal
      </MyBtn>
      <MyModal v-model:show="show">
        <MyInput disabled/>
        <MyInput disabled/>
        <MyBtn
            v-bind:value="post"
            @click="removeModal"
        >
          Delete
        </MyBtn>
      </MyModal>
    </div>

  </div>
</template>

<script>

export default {
  name: "PostItem",
  data() {
    return {
      show: false
    }
  },
  props: {
    post: {
      type: Object,
      required: true
    },
    // posts: {
    //   type: Array,
    //   required: true
    // }
  },
  methods: {
    showModal() {
      this.show = true;
    },
    removeModal() {
      this.$emit('removeModal', this.post)
    }

    // removePostFromModal() {
    //   this.posts = this.posts.filter(p => p.id !== this.post.id)
    //   console.log(this.post.id);
    //   console.log(this.posts);
    // }
  }
}
</script>

<style scoped>
.post {
  padding: 15px;
  border: none;
  box-shadow: 0 2px 5px 0 rgba(0,0,0,0.3);
  border-radius: 5px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: space-between;
}


</style>