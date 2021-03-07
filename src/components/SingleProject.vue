<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="actions">
      <h3 @click="toogleDetails">{{ project.title }}</h3>
      <div class="icons">
        <router-link :to="{ name: 'EditProject', params: { id: project.id } }">
          <span class="material-icons"> edit </span>
        </router-link>
        <span @click="deleteProject" class="material-icons delete">
          delete
        </span>
        <span
          @click="toogleComplete"
          class="material-icons tick"
          :class="{ complete: !project.complete }"
        >
          done
        </span>
      </div>
    </div>
    <div class="details" v-if="showDetails">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    project: Object,
  },
  data() {
    return {
      showDetails: false,
      uri: 'http://localhost:3000/projects/' + this.project.id,
    }
  },
  methods: {
    toogleDetails() {
      this.showDetails = !this.showDetails
    },
    deleteProject() {
      fetch(this.uri, { method: 'DELETE' })
        .then(() => this.$emit('deleteProject', this.project.id))
        .catch((err) => console.log(err))
    },
    toogleComplete() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ complete: !this.project.complete }),
      })
        .then(() => this.$emit('toogleComplete', this.project.id))
        .catch((err) => console.log(err))
    },
  },
}
</script>

<style>
.project {
  margin: 20px auto;
  background-color: #fff;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.3);
  border-left: 4px solid #e90074;
}

.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  cursor: pointer;
}

.material-icons {
  font-size: 24px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
  transition: color 0.1s ease-in;
}

.material-icons:hover {
  color: #777;
}

.material-icons.delete:hover {
  color: #c70000;
}

/* completed projects */
.project.complete {
  border-left: 4px solid #00ce89;
}

.material-icons.complete:hover {
  color: #00ce89;
}

.project.complete .tick {
  color: #00ce89;
}
</style>