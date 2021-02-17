<template>
  <div class="default">
    <vs-navbar v-model="active" shadow center-collapsed>
      <vs-navbar-item
        v-for="item in menu"
        :to="item.to"
        :id="item.slug"
        :active="active === item.slug"
        :key="item.slug"
      >
        {{ item.label }}
      </vs-navbar-item>
    </vs-navbar>
    <div class="default__content">
      <vs-row>
        <vs-col w="12">
          <Nuxt />
        </vs-col>
      </vs-row>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    active: 'home',
    menu: [
      {
        slug: 'home',
        to: '/',
        label: 'Эксперименты',
      },
      {
        slug: 'about',
        to: { name: 'about' },
        label: 'Обо мне',
      },
    ],
  }),
}
</script>

<style lang="scss" scoped>
.default {
  &__content {
    position: relative;
    height: 100vh;
    overflow: auto;
  }
}
</style>
