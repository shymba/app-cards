<template>
  <div class="app">
    <h2>Page with Cards</h2>
    <div class="app__btns">
      <MyBtn @click="showModal">Add Card</MyBtn>
      <MyBtn @click="deleteLast">Delete Last</MyBtn>
      <MyBtn @click="fillItems">Fill Items</MyBtn>
      <MyBtn @click="clearAll">Clear</MyBtn>
    </div>
    <MyModal v-model:show="modalVisible">
      <PostForm
          @create="createPost"
      />
    </MyModal>

    <PostList
        @remove="removePost"
        @removeModal="removePost"
        :posts="posts"
        v-if="!isLoading"
    />
    <div v-else style="color: green"><h2>Loading......</h2></div>
    <div ref="observer" class="observer"></div>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import axios from "axios";

export default {
  name: "App",
  components: {
    PostForm,
    PostList
  },
  data() {
    return {
      posts: [],
      modalVisible: false,
      isLoading: false,
      page: 1,
      id: null,
      limit: 10,
      totalPage: 0
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.modalVisible = false
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    showModal() {
      this.modalVisible = true;
    },
    fillItems() {
      this.fetchCarts()
    },
    clearAll() {
      this.posts = []
    },
    deleteLast() {
      this.posts.pop()
    },
    async fetchCarts() {
      try {
        this.isLoading = true;
          const resp = await axios.get('https://jsonplaceholder.typicode.com/posts', {
            params: {
              _page: this.page,
              _limit: this.limit
            }
          });
          this.totalPage = Math.ceil(resp.headers['x-total-count'] / this.limit)
          this.posts = resp.data;
      } catch (err) {
        console.log('Error >>', err)
      } finally {
        this.isLoading = false;
      }
    },
    async loadMore() {
      try {
        this.page += 1;
        const resp = await axios.get('https://jsonplaceholder.typicode.com/posts', {
          params: {
            _page: this.page,
            _limit: this.limit
          }
        });
        this.totalPage = Math.ceil(resp.headers['x-total-count'] / this.limit)
        this.posts = [...this.posts, ...resp.data];
      } catch (err) {
        console.log('Error >>', err)
      }
    }
  },
  mounted() {
    this.fetchCarts();
    const options = {
      rootMargin: '0px',
      threshold: 1.0
    }
    const callback = (entries, observer) => {
      if(entries[0].isIntersecting) {
        this.loadMore()
      }
    };
    const observer = new IntersectionObserver(callback, options);
    observer.observe(this.$refs.observer);
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app__btns {
  display: flex;
  margin: 20px 0;
}

</style>