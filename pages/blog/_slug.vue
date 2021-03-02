<template>
  <article class="blog-part">
        <nuxt-content :document="article" />
  </article>
</template>

<script>
  export default {
    async asyncData({ $content, params }) {
      const article = await $content('blog', params.slug).fetch()
      return {
        article
      }
    }
  }
</script>

<style>
.blog-part{
  @apply w-3/4 mx-auto
}

  .blog-part h1 {
      @apply text-gray-800 font-black text-3xl m-12 text-center font-sans 
  }

  .blog-part h2{
        @apply text-gray-600 italic font-semibold text-2xl border-b-2 border-gray-700 inline-block p-2
  }
  .blog-part p{
        @apply text-gray-900 text-xl font-normal
  }
</style>