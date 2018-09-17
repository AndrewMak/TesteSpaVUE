<template>
  <div id="app">
    <header>
      <h1>Spa VUE</h1>
    </header>
    <main>     
      <aside class="sidebar">
         <div>Menu</div>
        <ul>
        <router-link
            v-for="post in posts"
            active-class="is-active"
            class="link"
            :to="{ name: 'post', params: { id: post.id } }">
         <li> {{post.id}}. {{post.title}}</li>
        </router-link>
        </ul>
      </aside>
      <div class="content">
        <router-view></router-view>
      </div>
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

<style>
.sidebar{
display: block;
float: left;
width: 50%;

}
</style>
