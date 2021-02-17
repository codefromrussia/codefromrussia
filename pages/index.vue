<template>
  <div class="blog">
    <vs-card
      v-for="article of articles"
      :key="article.slug"
      @click="goToPost(article.slug)"
      class="blog__post"
    >
      <template #title>
        <h3>{{ article.title }}</h3>
      </template>
      <template #img>
        <img :src="article.img" alt="" />
      </template>
      <template #text>
        <p>
          {{ article.description }}
        </p>
      </template>
      <template #interactions>
        <vs-button danger icon>
          <i class="bx bx-heart"></i>
        </vs-button>
        <vs-button class="btn-chat" shadow primary>
          <i class="bx bx-chat"></i>
          <span class="span"> 54 </span>
        </vs-button>
      </template>
    </vs-card>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const articles = await $content('articles', params.slug)
      .only(['title', 'description', 'img', 'slug'])
      .sortBy('createdAt', 'asc')
      .fetch()

    return {
      articles,
    }
  },
  methods: {
    goToPost(slug) {
      this.$router.push({ name: 'blog-slug', params: { slug } })
    },
  },
}
</script>

<style lang="scss" scoped>
.blog {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 74px 30px 30px 30px;
  &__post {
    margin-bottom: 30px;
  }
}
</style>
