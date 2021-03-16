<template>
  <div class="container">
    <div class="header">
      <h1>devjobs</h1>
    </div>
    <div class="search">
      <div class="companyFilter">
        <input type="text" placeholder="Filter by title, companies, expertise" name="company" v-model="company">
      </div>
      <div class="locationFilter">
        <input type="text" placeholder="Filter by location..." name="location" v-model="location">
      </div>
      <div class="buttons">
        <input type="checkbox" name="checkbox" v-model="checkbox">
        <p>Full Time Only</p>
        <button type="submit" @click.stop.prevent="submit()">Search</button>
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
    <button class="loadMore">Load More</button>
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
      jobs: [],
      company: null,
      location: null,
      checkbox: null,
    }
  },
  methods: {
    submit() {
      this.jobs = [];
      axios.get(URL + "?description=" + this.company + "&location=" + this.location).then(res => {
        this.jobs = res.data;
      })

    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  text-align: center;
}

.header {
  display: flex;
  align-items: center;
  background-color: blue;
  color: white;
  min-height: 100px;
  border-bottom-left-radius: 50px;
  padding: 50px;
  padding-left: 250px;
}

.search {
  margin: 0 auto;
  margin-top: -20px;
  max-width: 700px;
  padding: 10px;
  border-radius: 10px;
  background-color: white;
  display: flex;
  justify-content: center;
  align-items: center;
}

.companyFilter {
  margin-right: 15px;
  border-right: 1px solid rgba(0, 0, 0, 0.15);
}

.companyFilter input {
  border: none;
  padding: 20px;
}

.locationFilter {
  margin-right: 15px;
  border-right: 1px solid rgba(0, 0, 0, 0.15);
}

.locationFilter input {
  border: none;
  padding: 20px;
  border-radius: 10px;
}

.buttons {
  display: flex;
  justify-content: center;
  align-items: center;
}

.buttons button {
  border: none;
  background-color: rgb(209, 0, 209);
  color: white;
  font-weight: 700;
  padding: 10px 20px;
  border-radius: 5px;
}

.buttons input {
  margin-right: 10px;
  border-radius: 10px;
}

.buttons p {
  margin-right: 10px;
}

.jobsection {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  padding: 250px;
  padding-top: 50px;
  padding-bottom: 20px;
}

.jobcard {
  text-align: left;
  flex: 1 0 30%;
  margin-bottom: 20px;
  margin-right: 10px;
  padding: 15px;
  max-width: 350px;
  min-height: 150px;
  box-shadow: 2px 2px 20px rgba(0, 0, 0, 0.192);
}

.jobcard h2 {
  font-size: 16px;
}

.jobcard p {
  opacity: 50%;
  font-size: 14px;
}

.companyLogo {
  width: 40px;
}

.loadMore {
  border: none;
  background-color: rgb(209, 0, 209);
  color: white;
  font-weight: 700;
  padding: 10px 20px;
  border-radius: 5px;
  margin-bottom: 20px;
}

</style>
