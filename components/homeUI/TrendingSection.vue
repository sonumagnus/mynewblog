<template>
  <div class="bg-gray-700 px-6 py-4 main-container">
    <div class="article" v-for="article of articles"  :key="article">
      <nuxt-link  :to="{ name: 'blog-slug', params: { slug: article.slug}}">
        <div class="article-inside">
          <img :src="require(`~/assets/resources/${article.img}`)" />
          <div class="article-detail">
            <h2>{{article.title}}</h2>
            <h3>{{article.description}}</h3>
          </div>
        </div>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      articles: [],
    };
  },
  async fetch(){
    this.articles = await this.$content('blog', params.slug)
    .only(['title', 'description', 'img', 'slug'])
    .sortBy('createdAt', 'asc')
    .limit(2)
    .fetch();
  }
}
</script>

<style>
 .main-container{
   @apply container p-5 flex justify-evenly
 }
  .article{
    @apply p-3
  }
  .article-inside{
    @apply h-72 w-60 bg-gray-50 py-2 rounded-lg
  }
  .article-inside img{
    @apply w-11/12 h-3/5 m-auto rounded-lg
  }
  .article-detail{
    @apply h-2/5
  }
  .article-detail h2{
    @apply text-lg font-bold text-center
  }
  .article-detail h3{
    @apply text-base font-semibold text-center
  }
</style>