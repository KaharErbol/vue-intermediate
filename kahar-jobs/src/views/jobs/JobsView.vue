<template>
  <h1>Jobs</h1>
  <div v-if="jobs.length">
    <div v-for="job in jobs" :key="job.id" class="job">
      <router-link :to="{ name: 'jobDetail', params: { id: job.id }}">
        <h2>{{ job.title }} - {{ job.id }}</h2>
      </router-link>
    </div>
  </div>
  <div v-else>
    <p>Loading ...</p>
  </div>
  
</template>

<script>
export default {
  data() {
    return {
      jobs: []
    }
  },
  async mounted() {
    try {
      const response = await fetch('http://localhost:3000/jobs')
      if (!response.ok) {
        throw new Error(`HTTP error! Status: ${response.status}`)
      }
      const data = await response.json()
      this.jobs = data
    } catch(error) {
      console.error('Error fetching data:', error);
      throw error;
    }
    
    
    
  }
}
</script>

<style>
  .job h2 {
    background: #f4f4f4;
    padding: 20px;
    border-radius: 10px;
    margin: 10px auto;
    max-width: 600px;
    cursor: pointer;
    color: #444;
  }

  .job h2:hover {
    background: #ddd;
  }

  .job a {
    text-decoration: none;
  }

</style>