<template>
  <div>
    <hero />
    <section class="section">
      <div class="container">
        <h1 class="title">Featured Courses</h1>
        <div class="columns">
          <div v-for="course in courses" :key="course._id" class="column is-one-quarter">
            <course-card :course="course"/>
          </div>
        </div>
      </div>
    </section>
    <section class="section">
      <div class="container">
        <h1 class="title">Featured Articles</h1>
        <div class="columns">
          <div class="column is-one-quarter">
            <blog-card />
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import Hero from "~/components/shared/Hero";
import CourseCard from "~/components/shared/CourseCard";
import BlogCard from "~/components/shared/BlogCard";
import {mapState} from 'vuex'

export default {
  components: {
    BlogCard,
    CourseCard,
    Hero,
    Logo
  },
  computed: {
      ...mapState({
        courses: state => state.course.items
      })
  },
  async fetch({store}){
    await store.dispatch('course/fetchCourses')
  }
}
</script>

<style lang="scss" scoped>
// Home page
.links {
  padding-top: 15px;
}
</style>