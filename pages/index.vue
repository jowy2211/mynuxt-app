<template>
  <div class="mt-5">
    <div class="container">
      <div class="card-columns">
        <div
          v-for="item in post"
          :key="item.id"
          class="card"
          @click="openDetail(item)"
        >
          <img :src="item.urlToImage" class="card-img-top" alt="Image Top" />
          <div class="card-body">
            <p class="card-text">
              {{ item.author }}
              <small class="text-muted">- {{ item.source.name }}</small>
            </p>
            <h5 class="card-title">{{ item.title }}</h5>
            <p class="card-text">
              <small class="text-muted">{{ item.description }}</small>
            </p>
          </div>
        </div>
      </div>
    </div>
    <button class="btn btn-md btn-info btn-more" @click="loadMore">
      Load More
    </button>
  </div>
</template>

<style lang="scss" scoped>
.btn-more {
  margin: 20px auto;
  display: block;
}

@media (min-width: 768px) {
  .card-columns {
    column-count: 3;
  }
}

@media (min-width: 992px) {
  .card-columns {
    column-count: 3;
  }
}

@media (min-width: 1200px) {
  .card-columns {
    column-count: 3;
  }
}
</style>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      allPost: [],
      post: [],
      current: 9
    }
  },
  mounted() {
    const apiKey = 'bafc80cf8d734e38a987e51768bef378'
    axios
      .get(
        `https://newsapi.org/v2/everything?q=programming&domains=techcrunch.com,techinasia.com&apiKey=` +
          apiKey,
        {
          crossDomain: true
        }
      )
      .then(({ data }) => {
        if (this.$store.state.article) {
          this.allPost = data.articles
          data.articles.map((item) => {
            if (item.description !== null && this.post.length < 9) {
              this.post.push(item)
            }
          })
        }
      })
      .catch((err) => {
        alert(err)
      })
  },
  methods: {
    loadMore() {
      this.post = []
      this.current += 9
      this.allPost.map((item, key) => {
        if (item.description !== null && this.post.length < this.current) {
          this.post.push(item)
        }
      })
    },
    openDetail(data) {
      this.$store.commit('setArticle', data)
      this.$router.replace({ path: '/detail' })
    }
  }
}
</script>
