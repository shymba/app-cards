<template>
  <form @submit.prevent>
    <h4>Create Card</h4>
    <MyInput
        v-model="post.title"
        type="text"
        placeholder="name"
    />
    <MyInput
        v-model="post.body"
        type="text"
        placeholder="description"
    />
    <MyBtn
        style="align-self: flex-end; margin-top: 15px"
        @click="createPost"
    >
      Add
    </MyBtn>
  </form>
</template>

<script>
export default {
  name: "PostForm",
  data() {
    return {
      post: {
        title: '',
        body: '',
        id: null
      }
    }
  },
  methods: {
    createPost() {
      this.post.id = Date.now();
      this.$emit('create', this.post)
      this.post = {
        title: '',
        body: ''
      }
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}

</style>