<template>
  <div class="container">
    <main>
      <h1>{{page.title}}</h1>
      <div class="content">
        <div v-html="page.html">{{ page.html }}</div>
      </div>
    </main>
  </div>
</template>

<script>
  import Logo from '~/components/Logo.vue'
  import { getPage } from '~/api/posts';


  export default {
      async asyncData () {
        const page = await getPage('who-am-i');
        return { page: page }
      },
      head () {
        return {
          title: this.page.meta_title,
          meta: [
            // hid is used as unique identifier. Do not use `vmid` for it as it will not work
            { hid: 'description', name: 'description', content: this.page.meta_description }
          ]
        }
      }
  }
</script>

<style>
  header {
    height: 15em;
  }

  h1 {
    color: white;
    margin-bottom: 1em;
  }

  .content {
    background: white;
    border-radius: 1em;
    padding: 1em;
  }

  main {
    margin-top: -9em;
  }

  .content img {
    width: 100%;
  }

@media only screen and (min-width: 768px) {
  .content {
    padding: 2em;
  }
}

</style>
