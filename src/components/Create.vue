<script src="https://unpkg.com/axios/dist/axios.min.js"></script>

<template>
  <b-container fluid>
    <b-row>
      <b-col sm="5" style="margin-top: 120px">
        <h1 style="font-size: 70px">Create New Project</h1>
      </b-col>
    </b-row>
    <b-row align-h="center">
      <b-col
        style="margin-top: 240px; max-width: 700px"
        align-self="center"
        xl="5"
        lg="6"
        md="7"
        sm="9"
      >
        <b-form @submit="onSubmit" @reset="onReset">
          <b-form-group id="title-group" label="Project Title:" label-for="title">
            <b-form-input
              id="title"
              v-model="form.title"
              type="text"
              required
              placeholder="Enter a title for your project"
            ></b-form-input>
          </b-form-group>

          <b-button style="margin: 2px" type="submit" variant="primary">Create Project</b-button>
        </b-form>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      form: {
        title: ''
      }
    };
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      alert(this.form.title);
      return {
        title: this.form.title
      };
    },
    methods: {
      onSubmit(evt) {
        evt.preventDefault();
        axios.post('http://localhost:3000/create', {
          title: this.form.title
        })
          .then(function(response) {
            alert(response);
          });
      },
      onReset(evt) {
        evt.preventDefault()
        // Reset our form values
        this.form.title = '';
      }
    }
  }
};
</script>
