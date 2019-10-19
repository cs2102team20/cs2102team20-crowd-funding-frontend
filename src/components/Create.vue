<template>
  <div class="create-form container fluid">
    <b-form @submit="onSubmit" @reset="onReset">
      <b-form-group id="input-group-project-title" label="Project Title:" label-for="input-project-title">
        <b-form-input
                id="input-project-title"
                v-model="form.projectTitle"
                type="text"
                required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-category" label="Category:" label-for="input-category">
        <b-form-select
                id="input-category"
                v-model="form.category"
                :options="categories"
                required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-image-url" label="Image Url:" label-for="input-image-url">
        <b-form-input
                id="input-image-url"
                v-model="form.imageUrl"
                placeholder="E.g. https://unsplash.com/photos/hD5HgJzhjG4"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-deadline" label="Project End Date:" label-for="input-deadline">
        <b-form-input
                id="input-deadline"
                v-model="form.deadline"
                type="date"
                required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-funding-goal" label="Funding Goal: " label-for="input-funding-goal">
        <b-form-input
                id="input-funding-goal"
                v-model="form.fundingGoal"
                type="number"
                required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-description" label="Project Description: " label-for="textarea-description">
        <b-form-textarea
                id="textarea-description"
                v-model="form.description"
                placeholder="Tell us more about your project..."
                rows="3"
                max-rows="16"
        ></b-form-textarea>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
    </b-form>
    <b-card class="mt-3" header="Form Data Result">
      <pre class="m-0">{{ form }}</pre>
    </b-card>
  </div>
</template>

<script>
  import axios from "axios";

  export default {
    data() {
      return {
        form: {
          projectTitle: '',
          category: '',
          imageUrl: '',
          deadline: '',
          fundingGoal: '',
          description: ''
        },
        categories: ['Arts', 'Crafts', 'Electronics', 'Games']
      }
    },
    methods: {
      onSubmit(evt) {
        evt.preventDefault()
        axios
                .post("http://localhost:3030/create", this.form)
                .then(response => response.json("Success"))
                .catch(error => alert(error))
        //alert(JSON.stringify(this.form))
      },
      onReset(evt) {
        evt.preventDefault()
        // Reset our form values
        this.form.email = ''
        this.form.name = ''
        this.form.food = null
        this.form.checked = []
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      }
    }
  }
</script>

<style>
  .create-form {
    text-align: left;
  }
</style>