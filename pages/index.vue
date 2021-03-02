<template>
  <div class="blog-section">
    <h2 class="font-bold text-2xl text-gray-600">Latest Post</h2>
    <div class="articles">
      <div class="article" v-for="article of articles"  :key="article">
        <nuxt-link :to="`/blog/${article.slug}`">
          <div class="article-inner">
            <img :src="require(`~/assets/resources/${article.img}`)" />
            <div class="detail">
              <h3>{{article.title}}</h3>
              <p>{{article.description}}</p>
            </div>
          </div>
        </nuxt-link>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  async asyncData({ $content, params}){
    const articles = await $content('blog', params.slug)
    .only(['title', 'description', 'img', 'slug'])
    .sortBy('createdAt', 'asc')
    .fetch();
    return{
      articles
    }
  }
}
</script>

<style scoped>

.blog-section {
  @apply py-14 md:px-8 px-0
}
h2 {
  @apply md:mb-8 mb-2 text-center
}
.articles {
  @apply my-0 mx-auto md:max-w-3xl
}
.article {
  @apply mb-4
}
.article-inner {
  @apply p-3 bg-gray-50 shadow-xl rounded-lg flex md:h-auto h-32 overflow-hidden 
}
.article-inner img {
  @apply block md:w-48 w-28 max-w-xs rounded-lg
}
.article-inner .detail {
  @apply px-4
}
h3 {
  @apply text-gray-800 md:text-2xl text-xl
}
p {
  @apply text-gray-400 text-xl
}
</style>