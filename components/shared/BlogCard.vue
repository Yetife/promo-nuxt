<template>
  <div class="card">
    <div class="card-content">
      <div class="media">
        <div class="media-content">
          <p class="title is-4">Some Super Title</p>
          <p class="subtitle is-6"><i>Some Super Subtitle</i></p>
        </div>
      </div>
      <div class="content">
        Some Description
        <br>
      </div>
    </div>
    <footer class="card-footer">
      <nuxt-link :to="'#'" class="card-footer-item">Read More</nuxt-link>
    </footer>
  </div>
</template>

<script>
export default {
  name: "BlogCard"
}
</script>

<style scoped>

</style>