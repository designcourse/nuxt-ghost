<template>
  <div>
    <div class="hero">
      <div class="container">
        <h1>Welcome to My Blog</h1>
        <p class="subtitle">Lorem, ipsum dolor sit amet consectetur adipisicing elit. Commodi, modi. Maxime explicabo neque odio facilis.</p>
        <nuxt-link to="/contact" class="hire">Hire me</nuxt-link>
      </div>
    </div>

    <div class="container">
      <main>
        <h2>Latest thoughts</h2>
        <ul>
          <li v-for="(post, index) in posts" :key="index">
            <img :src="post.feature_image">
            <div class="content">
              <span>{{ post.authors[0].name }}</span>
              <nuxt-link :to="{ path: post.slug }">{{ post.title }}</nuxt-link>
              <p>{{ post.excerpt }}</p>
            </div>
          </li>
        </ul>
      </main>
    </div>

  </div>
</template>

<script>

import { getPosts } from '~/api/posts';

export default {
  async asyncData () {
    const posts = await getPosts();
    return { posts: posts }
  }
}
</script>

<style lang="scss">

  .hero {
    background-color: $primary-color;
    color: white;
    text-align: center;
    padding-top: 2em;

    h1 {
      margin-bottom: 1em;
    }

    .hire {
      background: darken($primary-color, 10%);
      padding: .5em 3em;
      margin: 2em 0 3em;
      display: inline-block;
      border-radius: 10px;
      color: $accent-color;
      text-decoration: none;
    }
  }

  .container ul {
    list-style-type: none;
    padding: 0;
  }

  main {

    li {
      background: white;
      border-radius: 1em;
      padding: .8em;
      margin: 1em 0;
      box-shadow: 15px 21px 40px 0px rgba(0,0,0,0.04);
    }

    img {
      width: 100%;
      border-radius: .5em;
    }

    .content {
      padding: .5em;
    }

    a {
      font-size: 1.5em;
      text-decoration: none;
      color: black;
      font-weight: bold;
      display: block;
      margin: -.1em 0 .2em;
    }

    h2 {
      margin-top: 3em;
      text-transform: uppercase;
      font-size: .8em;
    }

    span {
      color: $primary-color;
      text-transform: uppercase;
    }

  }

@media only screen and (min-width: 768px) {
  main li {
    display: grid;
    grid-template-columns: 180px auto;
    grid-column-gap: 1em;
  }
}

</style>
