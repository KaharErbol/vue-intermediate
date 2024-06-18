<template>
  <div v-if="job">
    <h1>{{ job.title }}</h1>
    <p>The job ID is {{ id }}</p>
    <p>{{ job.details }}</p>
  </div>
  <div v-else>
    <p>Loading ...</p>
  </div>
</template>

<script>
export default {
  props: ['id'],
  data() {
    return {
      job: null
    }
  },
  async mounted() {
    try {
        const response = await fetch('http://localhost:3000/jobs/' + this.id)
        if (!response.ok) {
          throw new Error(`HTTP error! Status: ${response.status}`)
        }
        const data = await response.json()
        this.job = data
    } catch(error) {
        console.error('Error fetching data:', error);
        throw error;
    }
  }
}

</script>

<style>

</style>