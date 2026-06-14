<template>
  <h2>user Posts</h2>
  <div class="search">
    <input type="search" placeholder="Search post" v-model="search" />
  </div>
  <p v-if="loading">Loading post...</p>

  <p v-else-if="error">{{ error }}</p>

  <div v-else class="posts">
    <div class="post" v-for="post in filteredPosts" :key="post.id">
      <h2>{{ post.title }}</h2>
      <p>{{ post.body }}</p>
    </div>
    <p v-if="filteredPosts.length === 0">No post available!</p>
  </div>
</template>

<script setup>
import { computed, onMounted, ref, watch } from "vue";

const posts = ref([]);
const loading = ref(false);
const error = ref("");
const search = ref("");
const debounceValue = ref("");

const fetchPosts = async () => {
  try {
    loading.value = true;
    const response = await fetch("https://jsonplaceholder.typicode.com/posts");
    if (!response.ok) {
      throw new Error("Failed to fetch posts");
    }
    const result = await response.json();
    posts.value = result;
  } catch (err) {
    error.value = err.message;
  } finally {
    loading.value = false;
  }
};


watch(search, (newValue) => {
    let timer = setTimeout(() => {
        debounceValue.value = newValue
    }, 600);

    return () => clearTimeout(timer);
})

const filteredPosts = computed(() => {
  return posts.value.filter((post) =>
    post.title.toLowerCase().includes(debounceValue.value.toLowerCase()),
  );
});

onMounted(() => {
  fetchPosts();
});
</script>
