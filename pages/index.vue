<template>
  <div class="container">
    <div class="header">
      <h1>devjobs</h1>
    </div>
    <div class="search">
      <div class="companyFilter">
        <input type="text" placeholder="Filter by title, companies, expertise">
      </div>
      <div class="locationFilter">
        <input type="text" placeholder="Filter by location...">
      </div>
      <div class="buttons">
        <input type="checkbox">
        <p>Full Time Only</p>
        <input type="button" value="Search">
      </div>
    </div>
    <div class="jobsection">
      <div v-for="job in jobs" :key="job.id" class="jobcard">
        <img class="companyLogo" :src="job.company_logo" alt="">
        <p> {{ job.type }} </p>
        <h2> {{ job.title }} </h2>
        <p> {{ job.company }}</p>
        <p class="location"> {{ job.location }} </p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

const URL = 'https://jobs.github.com/positions.json'

export default {
  async asyncData ({}) {
    const res = await axios.get(URL)
    return { jobs: res.data }
  },
  data () {
    return {
      jobs: []
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
}

.header {
  display: flex;
  align-items: center;
  background-color: blue;
  color: white;
  min-height: 100px;
  border-bottom-left-radius: 50px;
  padding: 50px;
}

.search {
  margin: 0 auto;
  margin-top: -20px;
  max-width: 600px;
  padding: 10px;
  border-radius: 10px;
  background-color: white;
  display: flex;
  justify-content: center;
  align-items: center;
}

.companyFilter {
  margin-right: 10px;
}

.companyFilter input {
  border: none;
}

.locationFilter {
  margin-right: 10px;
}

.locationFilter input {
  border: none;
}

.buttons {
  display: flex;
  justify-content: center;
  align-items: center;
  
}

.jobsection {
  display: flex;
  flex-wrap: wrap;
  padding: 50px;
}

.jobcard {
  margin-top: 10px;
  margin-right: 10px;
  padding: 15px;
  width: 350px;
  box-shadow: 2px 2px 20px rgba(0, 0, 0, 0.192);
}

.companyLogo {
  width: 40px;
  border-radius: 5px;
}

</style>
