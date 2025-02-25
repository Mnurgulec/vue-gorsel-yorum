<template>
  <div>

    <form @submit.prevent="post">
      <div class="input-group">
        <input
          v-model="postContent"
          class="form-control"
          type="text"
          name="content"
          placeholder="Bir şeyler yaz."
        />
        <span class="input-group-btn">
          <button class="btn btn-success" type="submit" name="post">
            Yayınla
          </button>
        </span>
      </div>
      
    </ form>
    <hr />


    <div>
      <div
        class="panel panel-default"
        v-for="(post, index) in posts"
        :key="index"
      >
        <div class="panel-body">
          <p>{{ post.content }}</p>
        </div>
        <div class="panel-footer">
          <span>posted {{ post.date }}</span>
          <span class="pull-right">
            <a class="text-danger" href="#" @click.prevent="deletePost(index)">[delete]</a>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted, watch } from "vue";

export default {
  setup() 
  {
    const postContent = ref("");
    const posts = ref([]);


    onMounted(() => {
      const savedPosts = localStorage.getItem("posts");
      console.log("LocalStorage'dan gelen:", savedPosts); // **Hata ayıklama için log ekledik**
      
      if (savedPosts) {
        try {
          posts.value = JSON.parse(savedPosts) || [];
        } catch (e) {
          console.error("Hata JSON parse edilirken:", e);
          posts.value = [];
        }
      }
    });


    const updateStorage = () => {
      localStorage.setItem("posts", JSON.stringify(posts.value));
      console.log("Güncellenen LocalStorage:", localStorage.getItem("posts")); // **LocalStorage güncellenmesini test et**
    };


    const post = () => {
      const trimmedContent = postContent.value.trim();
      if (trimmedContent) {
        posts.value.push({
          content: trimmedContent,
          date: new Date().toLocaleString(),
        });
        postContent.value = "";
        updateStorage(); 
      }

    };


    const deletePost = (index) => {
      posts.value.splice(index, 1);
      updateStorage(); 
    };

    watch(posts, updateStorage, { deep: true });

    return {

        postContent,
        posts,
        post,
        deletePost,
    };
  },
};


</script>

<style scoped>
.input-group {
  margin-bottom: 15px;
}
.panel {
  margin-bottom: 15px;
}
</style>
