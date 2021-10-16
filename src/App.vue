<template>
  <!-- 
    install axios by typing this in the terminal:
    npm install axios

    https://api.npms.io/v2/search?q=vue
    http://jsonplaceholder.typicode.com/posts
   -->
  <div>
    <h2>Total vue packages</h2>
    <div>
      {{ totalVuePackages }}
    </div>
    <h2>Posts from jsonplaceholder</h2>
    <div id="posts">
      <div v-for="post in posts" v-bind:key="post.id" class="post">
        <h3>{{ post.title }}</h3>
        <p>{{ post.body }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  components: {},
  data() {
    return {
      totalVuePackages: null,
      posts: null,
    };
  },
  created() {
    axios
      .get("https://api.npms.io/v2/search?q=vue")
      .then((response) => (this.totalVuePackages = response.data.total));

    axios
      .get("http://jsonplaceholder.typicode.com/posts")
      .then((response) => (this.posts = response.data));
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin: 60px;
}

#posts {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

div,
h2 {
  margin: 20px 0;
}

.post {
  width: 20%;
  padding: 2.5%;
  margin: 0;
  transition: transform .2s ease-in;
  background-color: rgba(0,0,0,.2);
}

.post:hover {
  transform: scale(1.1);
}

.post:nth-child(3n){
  background-color: rgba(0,0,0,.3);
}

.post:nth-child(3n+1){
  background-color: rgba(0,0,0,.1);
}
</style>
