<template>
  <div>
    <nav class="navbar navbar-expand-sm bg-light">
      <ul v-if="!$store.state.article.title" class="navbar-nav">
        <li class="navbar-item">
          <nuxt-link to="/" class="nav-link">Home</nuxt-link>
        </li>
        <li class="navbar-item">
          <nuxt-link to="contacts" class="nav-link">My Contacts</nuxt-link>
        </li>
      </ul>
      <ul v-else class="navbar-nav">
        <li class="navbar-item">
          <a class="nav-link" href="#" @click="goBack()">
            Back
            <span class="ion-android-arrow-back"></span>
          </a>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  methods: {
    goBack() {
      this.$store.commit('setArticle', {})
      this.$router.replace({ path: '/' })
    }
  }
}
</script>
