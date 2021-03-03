<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject
          :project="project"
          @deleteProject="deleteProject"
          @toogleComplete="toogleComplete"
        />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject.vue'

export default {
  components: { SingleProject },
  name: 'Home',
  data() {
    return {
      projects: [],
    }
  },
  methods: {
    deleteProject(id) {
      this.projects = this.projects.filter((project) => project.id !== id)
    },
    toogleComplete(id) {
      let p = this.projects.find((project) => project.id === id)
      p.complete = !p.complete
    },
  },
  mounted() {
    fetch('http://localhost:3000/projects')
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err.message))
  },
}
</script>
