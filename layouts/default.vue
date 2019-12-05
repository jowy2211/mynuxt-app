<template>
  <div>
    <Navigation />
    <div class="container content">
      <nuxt />
    </div>

    <div class="footer">
      Footer
    </div>
  </div>
</template>

<script>
import Navigation from '~/components/Navigation'
export default {
  components: {
    Navigation
  }
}
</script>
