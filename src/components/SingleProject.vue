<template>
  <div class="project">
    <div class="actions">
      <h3 @click="toogleDetails">{{ project.title }}</h3>
      <div class="icons">
        <span class="material-icons"> edit </span>
        <span class="material-icons"> delete </span>
        <span class="material-icons"> done </span>
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
    }
  },
  methods: {
    toogleDetails() {
      this.showDetails = !this.showDetails
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
</style>