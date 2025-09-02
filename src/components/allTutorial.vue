<template>
<div>
    <h1>List Tutorial</h1>
    <input type="text" placeholder="Search by title" v-model="this.title"/>
    <button @click="search">Search</button>
    
</div>
<div v-if="tutorials.length > 0">
    <table border="1" cellpadding="5" cellspacing="0">
      <thead>
        <tr>
          <th>#</th>
          <th>Title</th>
          <th>Description</th>
          <th>Status</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(tutorial, index) in tutorials" :key="tutorial.id">
          <td>{{ index + 1 }}</td>
          <td>{{ tutorial.title }}</td>
          <td>{{ tutorial.description }}</td>
          <td>{{ tutorial.published ? "Published" : "Pending" }}</td>
          <td></td>
        </tr>
      </tbody>
    </table>
  </div>
  <div v-if="tutorials.length === 0">
    <br/>
    <h1>
    <p>No Data found !!</p>
    <img src="@/assets/logo.png" width="100px" height="50px" alt="No data" />
    </h1>
  </div>
</template>

<script>
import TutorialDataService from "../services/TutorialDataService";

    export default {
        name: "allTutorial",
        data() {
            return {
                title: "",
                tutorials: [],
                currentTutorial: null,
                currentIndex: -1,
            };
        },
        methods: {
            search() {
                alert("search for " + this.title);
                TutorialDataService.findByTitle(this.title).then(response => {
                   this.tutorials = response.data;
                    console.log(response.data);
                      console.log(this.tutorials);
                }).catch(e => {
                    console.log(e);
                });
            },
        },
    };
</script>
<style>
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 15px;
}
th {
  background-color: #f0f0f0;
}
td,
th {
  border: 1px solid #ccc;
  padding: 8px;
  text-align: left;
}
</style>