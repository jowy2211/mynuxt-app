<template>
  <div>
    <div class="contacts-layout">
      <div class="contacts-header">
        <nuxt-link to="/contacts" class="button-cancel">Cancel</nuxt-link>
      </div>
      <div class="contacts-main">
        <p>{{ detail }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import Axios from 'axios'
export default {
  data() {
    return {
      detail: {},
      params: this.$route.query.detail ? this.$route.query.detail : null
    }
  },
  mounted() {
    Axios.get(`https://maindata.herokuapp.com/users/${this.params}`)
      .then(({ data, status }) => {
        if (status === 200) {
          this.detail = data.result
        }
      })
      .catch((err) => {
        alert(err)
      })
  },
  layout: 'main'
}
</script>
