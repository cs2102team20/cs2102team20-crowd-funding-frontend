<template>
  <b-container class="bv-example-row">
    <br />
    <b-row class="text-center">
      <b-col cols="12">
        <b-img
          src="https://picsum.photos/seed/picsum/200/300"
          v-bind="mainProps"
          rounded="circle"
          alt="Center Circle image"
        ></b-img>
      </b-col>
    </b-row>
    <br/>
    <b-row class="text-center">
      <b-col cols="12">
        <b-button
          v-if="isUser == false && isFollowed == false"
          variant="success"
          @click="follow"
        >Follow</b-button>
        <b-button
          v-if="isUser == false && isFollowed == true"
          variant="danger"
          @click="unfollow"
        >Unfollow</b-button>
        <b-button v-if="isUser == true" variant="success" @click="goToWallet">Wallet</b-button>
      </b-col>
    </b-row>
    <br />
    <br />
    <b-row class="text-center">
      <b-col>
        <h3>Created {{numOfCreatedProjects}} projects</h3>
      </b-col>
      <b-col>
        <h3>Backed {{numOfBackedProjects}} projects</h3>
      </b-col>
    </b-row>

    <br />
    <br />
    <div v-if="this.$store.state.auth.isLoggedIn">
      <b-tabs content-class="mt-3" fill>
        <b-tab title="Projects Backed">
          <!-- Project Backed -->
          <projects-backed-section v-bind:backedProjects="backedProjects" />
        </b-tab>
        <b-tab title="Projects Created">
          <!-- Projects Created -->
          <projects-created-section
            v-bind:createdProjects="createdProjects"
            @delete:createdProject="deleteCreatedProject"
            @redeem:projectFunds="redeemProjectFunds"
          />
        </b-tab>
        <b-tab title="Search History" active v-if="isUser">
          <b-button
            class="mb-4"
            variant="success"
            v-on:click="clearSearchHistory"
          >Clear search history</b-button>
          <b-table striped hover :items="this.searchHistory" :fields="this.searchFields"></b-table>
        </b-tab>
      </b-tabs>
    </div>
    <div v-else>
      <p>Please log in dude.</p>
    </div>
  </b-container>
</template>
<script>
import axios from "axios";
import ProjectsBackedSection from "../sub-components/ProjectsBackedSection";
import ProjectsCreatedSection from "../sub-components/ProjectsCreatedSection";

export default {
  name: "Profile",
  components: {
    ProjectsBackedSection,
    ProjectsCreatedSection
  },
  data() {
    return {
      feedback: "",
      mainProps: {
        blank: false,
        blankColor: "#777",
        width: 250,
        height: 250,
        class: "m1"
      },
      backedProjects: [],
      createdProjects: [],
      isFollowed: null,
      searchHistory: [],
      searchFields: ["search_timestamp", "search_text"],
      feedBacks:[]
    };
  },
  mounted() {
    this.loadIsFollowed();
    this.loadBackedProjects();
    this.loadCreatedProjects();
    this.loadSearchHistory();
    this.loadFeedBack();
  },
  computed: {
    numOfBackedProjects() {
      return this.backedProjects.length;
    },
    numOfCreatedProjects() {
      return this.createdProjects.length;
    },
    isUser() {
      return this.$store.state.user.email == this.$route.params.email;
    }
  },
  methods: {
    loadFeedBack() {
      axios.get("http://localhost:3000/feedback" + this.$route.params.email)
    },
    loadIsFollowed() {
      console.log(
        "http://localhost:3000/profile/follows/" +
          this.$store.state.user.email +
          "/" +
          this.$route.params.email
      );
      axios
        .get(
          "http://localhost:3000/profile/follows/" +
            this.$store.state.user.email +
            "/" +
            this.$route.params.email
        )
        .then(res => {
          this.isFollowed = Object.entries(res.data).length > 0;
          console.log(res.data);
        });
    },
    clearSearchHistory() {
      if (this.searchHistory.length === 0) {
        alert("Your Search History is empty!");
        return;
      }
      axios
        .post("http://localhost:3000/search/clear", {
          email: this.$store.state.user.email
        })
        .then(response => {
          if (response.data == "success") {
            alert("Your Search History has been cleared!");
            this.loadSearchHistory();
          } else {
            alert("Internal Server Error");
          }
        });
    },
    loadSearchHistory() {
      axios
        .get(
          "http://localhost:3000/search/history/" + this.$store.state.user.email
        )
        .then(response => {
          this.searchHistory = response.data;
        })
        .catch(error => {
          alert(error);
        });
    },
    loadBackedProjects() {
      axios
        .get(
          "http://localhost:3000/profile/" +
            this.$route.params.email +
            "/backedProjects"
        )
        .then(response => {
          // console.log(response.data);
          this.backedProjects = response.data;
          console.log(this.backedProjects);
        })
        .catch(error => {
          alert(error);
        });
    },
    loadCreatedProjects() {
      axios
        .get(
          "http://localhost:3000/profile/" +
            this.$route.params.email +
            "/createdProjects"
        )
        .then(response => {
          // console.log(response.data);
          this.createdProjects = response.data;
          console.log(this.createdProjects);
        })
        .catch(error => {
          alert(error);
        });
    },
    clearSearchHistory() {
      if (this.searchHistory.length === 0) {
        alert("Your Search History is empty!");
        return;
      }
      axios
        .post("http://localhost:3000/search/clear", {
          email: this.$store.state.user.email
        })
        .then(response => {
          if (response.data == "success") {
            alert("Your Search History has been cleared!");
            this.loadSearchHistory();
          } else {
            alert("Internal Server Error");
          }
        });
    },
    loadSearchHistory() {
      axios
        .get(
          "http://localhost:3000/search/history/" + this.$store.state.user.email
        )
        .then(response => {
          this.searchHistory = response.data;
        })
        .catch(error => {
          alert(error);
        });
    },
    deleteCreatedProject(projectName) {
      axios
        .delete(
          "http://localhost:3000/profile/deleteCreatedProject/" +
            this.$store.state.user.email +
            "/" +
            projectName
        )
        .then(response => {
          //this.$set(this.projectNames, 0, parsedProjectName)
          //this.projectNames.push(parsedProjectName)
          //console.log(this.projectNames.toString());
          alert(response.data);
          // this.$router.push("/project/" + form.projectName);
          for (let i = 0; i < this.createdProjects.length; i++) {
            if (this.createdProjects[i].project_name == projectName) {
              this.$delete(this.createdProjects, i);
              break;
            }
          }
        })
        .catch(error => {
          // console.log(error.response.data);
          alert(error.response.data);
        });
    },
    follow() {
      alert(this.$route.params.email);
      axios
        .post("http://localhost:3000/profile/follows", {
          follower_id: this.$store.state.user.email,
          following_id: this.$route.params.email
        })
        .then(response => {
          //this.$set(this.projectNames, 0, parsedProjectName)
          //this.projectNames.push(parsedProjectName)
          //console.log(this.projectNames.toString());
          alert("Followed !");
          this.isFollowed = !this.isFollowed;
        })
        .catch(error => {
          // console.log(error.response.data);
          alert(error.response.data);
        });
    },
    unfollow() {
      axios
        .delete(
          "http://localhost:3000/profile/follows/" +
            this.$store.state.user.email +
            "/" +
            this.$route.params.email
        )
        .then(response => {
          //this.$set(this.projectNames, 0, parsedProjectName)
          //this.projectNames.push(parsedProjectName)
          //console.log(this.projectNames.toString());
          alert("Unfollowed !");
          this.isFollowed = !this.isFollowed;
        })
        .catch(error => {
          // console.log(error.response.data);
          alert(error.response.data);
        });
    },
    goToWallet() {
      this.$router.push("/profile/wallet");
    },
    redeemProjectFunds(project) {
      alert("Redeeming funds from profile");
      console.log("project")
      console.log(project)
      axios
              .post("http://localhost:3000/profile/transferProjectFundsToCreator", {
                creatorEmail: project.email,
                projectName: project.project_name
              })
              .then(res => {
                alert("Transfer success!")
              })
              .catch(error => {
                alert("Error: Unable to transfer project funds to creator.")
              })
    }
  }
};
</script>

<style>
</style>