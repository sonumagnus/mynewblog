<template>
  <div class="blog-section">
    <h2 class="font-bold text-2xl text-gray-600">Latest Post</h2>
    <div class="articles">
      <div class="article" v-for="article of articles"  :key="article">
        <nuxt-link :to="{ name: 'blog-slug', params: { slug: article.slug}}">
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
  @apply py-14 px-8
}
h2 {
  @apply mb-8 text-center
}
.articles {
  @apply my-0 mx-auto max-w-3xl
}
.article {
  @apply mb-4
}
.article-inner {
  @apply p-4 bg-gray-50 shadow-xl rounded-lg flex
}
.article-inner img {
  @apply block w-48 max-w-xs
}
.article-inner .detail {
  @apply px-4
}
h3 {
  @apply text-gray-800 text-2xl
}
p {
  @apply text-gray-400 text-xl
}
</style>