<template>
  <NavBar @searchEventHandle="searchEventHandle" @inputEventHandle="inputEventHandle" />

  <div class="container-min">
    <ul>
      <li style="list-style-type: disc" v-for="post in posts" :key="post.id">{{ post }}</li>
    </ul>

    <div>Posts: {{ posts.length }}</div>

    <input type="text" v-model="addPostContent" />
    <TheButton @click="addPost">Add Post</TheButton>
  </div>

  <TheButton disabled @click="btnHandler">取消</TheButton>

  <TheButton @click="showModal = true">SignIn</TheButton>
  <SigninForm
    v-if="showModal"
    :isVisible="showModal"
    @close="showModal = false"
    @submit="handleSubmit"
  />
</template>

<script>
import NavBar from "../components/layout/NavBar.vue";
import TheButton from "../components/common/TheButton.vue";
import SigninForm from "../components/layout/SigninForm.vue";

export default {
  components: { NavBar, TheButton, SigninForm },
  data() {
    return {
      posts: ["Post1", "Post2", "Post3"],
      originalPosts: ["Post1", "Post2", "Post3"],
      addPostContent: "",
      showModal: false,
    };
  },
  methods: {
    searchEventHandle(e) {
      this.posts = this.originalPosts.filter((post) => post.includes(e));
    },
    inputEventHandle(e) {
      if (e === "") {
        this.posts = [...this.originalPosts];
      }
    },
    addPost() {
      this.posts.push(this.addPostContent);
    },
    btnHandler() {
      console.log("我取消了");
    },
    handleSubmit(formData) {
      console.log("Form data received:", formData);
    },
  },
};
</script>

<style scoped></style>
