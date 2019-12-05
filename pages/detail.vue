<template>
  <div class="mt-5">
    <div class="container">
      <div class="row justify-content-md-center">
        <img :src="article.urlToImage" class="card-img-top" alt="Card Image" />
        <div class="col-8">
          <p class="card-text">
            {{ article.author }}
            <small class="text-muted">- {{ article.source.name }}</small>
            <small class="text-muted">- {{ article.publishedAt }}</small>
          </p>
          <h5 class="card-title">{{ article.title }}</h5>
          <p class="card-text">{{ article.description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    article() {
      return this.$store.state.article
    }
  }
}
</script>
