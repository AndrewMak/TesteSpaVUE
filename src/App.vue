<template>
  <div id="app">
    <header>
      <h1>Spa VUE</h1>
    </header>
    <main>

      <aside class="sidebar">
              <div class="content">
        <router-view></router-view>
      </div>
         <div class="col-md-3 mb-2">Menu</div>
       <div class="card-columns">
  <b-card v-for="post in posts"
          :title="post.title"
          img-src="https://picsum.photos/600/300/?image=25"
          img-alt="Image"
          img-top
          tag="article"
          style="max-width: 20rem;"
          class="mb-2">
    <p class="card-text">
     {{post.body}}
    </p>

    <b-button href="#" :to="{ name: 'post', params: { id: post.id } }" variant="warning">Visualizar Post</b-button>
  </b-card>
</div>
      </aside>

    </main>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    data () {
      return {
        posts: [],
        endpoint: 'https://jsonplaceholder.typicode.com/posts/',
      }
    },

    created() {
      this.getAllPosts();
    },

    methods: {
      getAllPosts() {
        axios.get(this.endpoint)
          .then(response => {
            this.posts = response.data;
          })
          .catch(error => {
            console.log('-----error-------');
            console.log(error);
          })
      }
    }
  }
</script>

<style lang="scss">
@import './assets/styles/variables';
@import './assets/styles/bootstrap';
</style>

