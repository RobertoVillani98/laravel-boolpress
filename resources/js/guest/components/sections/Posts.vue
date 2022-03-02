<template>
  <section>
    <h2 class="mt-3">Lista Posts</h2>
    <ul>
      <li class="my-3" v-for="post in posts" :key="post.id">
        <h3>{{ post.title }}</h3>
        <p v-if="post.category">
          <strong>Category:</strong> {{ post.category.name }}
        </p>
        <div v-if="post.tags.length > 0">
          <strong>Tags</strong>
          <ul>
            <li v-for="tag in post.tags" :key="tag.id">
              {{ tag.name }}
            </li>
          </ul>
        </div>
        <p>{{ post.content }}</p>
        <router-link :to="{ name: 'single-post', params: { slug: post.slug } }"
          >Show Post</router-link
        >
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  name: "Posts",
  data() {
    return {
      posts: [],
    };
  },
  created() {
    axios.get("/api/posts").then((response) => {
      this.posts = response.data;
    });
  },
};
</script>

<style>
</style>