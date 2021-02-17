<template>
  <article class="post">
    <div class="post__left">
      <div
        class="post__img"
        :style="`background-image: url(/${article.img})`"
      ></div>
    </div>
    <div class="post__right">
      <h1>{{ article.title }}</h1>
      <nuxt-content :document="article" />
      <prev-next :prev="prev" :next="next" />
    </div>
  </article>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const article = await $content('articles', params.slug).fetch()

    const [prev, next] = await $content('articles')
      .only(['title', 'slug'])
      .sortBy('createdAt', 'asc')
      .surround(params.slug)
      .fetch()

    return {
      article,
      prev,
      next,
    }
  },
}
</script>

<style lang="scss" scoped>
.post {
  display: flex;
  flex-wrap: wrap;
  height: 100vh;
  &__left {
    width: 40%;
    overflow: hidden;
  }
  &__img {
    height: 100%;
    background-position: center;
    background-size: cover;
    transition: all .3s ease;
    &:hover {
      transform: scale(1.2);
    }
  }
  &__right {
    width: 60%;
    padding: 74px 30px 30px 30px;
  }
}
</style>
