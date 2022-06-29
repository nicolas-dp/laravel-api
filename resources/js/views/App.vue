<template>
  <div>
    <work-in-progress></work-in-progress>
    <section class="posts">
      <div class="container">
        <div class="row">
          <div class="col" v-for="post in posts" :key="post.id">
            <div class="prodct card">
              <img :src="post.cover_image" :alt="post.title" />
              <div class="card-body">
                <h3>{{ post.name }}</h3>
                <small>{{ post.content }}</small>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>


<script>
import WorkInProgress from "../components/WorkInProgress";
export default {
  name: "App",
  components: { WorkInProgress },
  data() {
    return {
      posts: "",
      postsResponse: "",
      categories: "",
      tags: "",
    };
  },

  methods: {
    getAllPosts(postPage) {
      axios
        .get("api/posts", {
          params: {
            page: postPage,
          },
        })
        .then((response) => {
          //console.log(response);
          this.postsResponse = response.data.data;
          console.log(this.postsResponse);
        })
        .catch((e) => {
          console.log(e);
        });
    },
    getAllCategories() {
      axios
        .get("api/categories")
        .then((response) => {
          console.log(response);
          this.categories = response.data;
        })
        .catch((e) => {
          console.log(e);
        });
    },
    getAllTags() {
      axios
        .get("api/tags")
        .then((response) => {
          console.log(response);
          this.tags = response.data;
        })
        .catch((e) => {
          console.log(e);
        });
    },
  },

  mounted() {
    console.log("mounted");
    this.getAllPosts(1);
    this.getAllCategories();
    this.getAllTags();
  }
}
</script>
