<template>
  <div class="submit-form">
    <div v-if="!submitted">
      <div class="form-group">
        <label for="title">Title</label>
        <input
          type="text"
          class="form-control"
          id="title"
          required
          v-model="tutorial.title"
          name="title"
        />
      </div>

      <div class="form-group">
        <label for="description">Description</label>
        <input
          class="form-control"
          id="description"
          required
          v-model="tutorial.description"
          name="description"
        />
      </div>

       <div class="form-group">
        <label for="description">Image</label>
        <input
            type="file"
            class="form-control"
            id="image"
            accept="image/*"
            @change="onFileChange"
  />
      </div>

      
       <div class="form-group">
        <label for="description">PDF</label>
        <input
            type="file"
            class="form-control"
            id="pdf"
           accept="application/pdf"
            @change="onPDFFileChange"
  />
      </div>

      

      <button @click="saveTutorial" class="btn btn-success">Submit</button>
    </div>

    <div v-else>
      <h4>You submitted successfully!</h4>
      <button class="btn btn-success" @click="newTutorial">Add</button>
    </div>
  </div>
</template>

<script>
import TutorialDataService from "../services/TutorialDataService";

export default {
  name: "add-tutorial",
  data() {
    return {
      tutorial: {
        id: null,
        title: "",
        description: "",
        published: false,
        imageContent: null,
        pdfContent: null
      },
      submitted: false
    };
  },
  methods: {
    saveTutorial() {
      var data = {
        title: this.tutorial.title,
        description: this.tutorial.description,
        imageContent: this.tutorial.imageContent,
        pdfContent:this.tutorial.pdfContent
      };

      TutorialDataService.create(data)
        .then(response => {
          this.tutorial.id = response.data.id;
          console.log(response.data);
          this.submitted = true;
        })
        .catch(e => {
          console.log(e);
        });
    },
    
    newTutorial() {
      this.submitted = false;
      this.tutorial = {};
    },
    onFileChange(event) {
    const file = event.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onload = e => {
        this.tutorial.imageContent = e.target.result; // base64
      };
      reader.readAsDataURL(file);
    }
  },
  onPDFFileChange(event) {
    const file = event.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onload = e => {
        this.tutorial.pdfContent = e.target.result; // base64
      };
      reader.readAsDataURL(file);
    }
  }
  }
};
</script>

<style>
.submit-form {
  max-width: 300px;
  margin: auto;
}
</style>