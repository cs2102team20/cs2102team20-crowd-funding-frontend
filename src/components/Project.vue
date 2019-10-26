<template>
    <div>
        <b-jumbotron header="Project Title" lead="Project Description">
            <!-- Project Image  -->
            <b-card img-src="https://placekitten.com/300/300" img-alt="Card image" img-left class="mb-3">
                <b-card-text>
                    <h1>$50,000 CURRENT FUNDING</h1>
                    <p>pledged of $25,000 funding goal</p>
                </b-card-text>
                <b-card-text>
                    <h3>3,322</h3>
                    <p>backers</p>
                </b-card-text>
                <b-card-text>
                    <h3>13</h3>
                    <p>days to go</p>
                </b-card-text>
                <p>
                    <b-button variant="success">Back this project</b-button>
                </p>
                <p>
                    <b-button variant="outline-secondary"><i class="fa fa-heart" aria-hidden="true"></i> Like</b-button>
                </p>
                <p>This project will only be funding if it reaches its goal by (PROJECT_DEADLINE)</p>
            </b-card>
        </b-jumbotron>

        <!-- Navigation between Campaign | Project Update | Feedback | Comments -->
        <div class="nav-bar">
            <b-nav tabs fill>
                <b-nav-item active>Campaign</b-nav-item>
                <b-nav-item>Project Update</b-nav-item>
                <b-nav-item>Feedback</b-nav-item>
                <b-nav-item disabled>Comments</b-nav-item>
            </b-nav>
        </div>

        <!-- Description and Rewards -->
        <b-container class="bv-example-row">
            <b-row>
                <b-col cols="8">
                    <h2>Project Description</h2>
                    <p>
                        Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been
                        the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley
                        of type and scrambled it to make a type specimen book. It has survived not only five centuries,
                        but also the leap into electronic typesetting, remaining essentially unchanged. It was
                        popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages,
                        and more recently with desktop publishing software like Aldus PageMaker including versions of
                        Lorem Ipsum.
                    </p>
                </b-col>
                <b-col>
                    <h2>Rewards</h2>
                    <b-card
                            title="Pledge $40"
                            tag="article"
                            style="max-width: 20rem;"
                            class="mb-2"
                    >
                        <b-card-text>
                            <h6>Reward Name</h6>
                            <p>
                                Some quick example text to build on the card title and make up the bulk of the card's content.
                                Some quick example text to build on the card title and make up the bulk of the card's content.
                            </p>
                        </b-card-text>
                        <b-button href="#" variant="primary">Pledge</b-button>
                    </b-card>
                    <b-card
                            title="Pledge $40"
                            tag="article"
                            style="max-width: 20rem;"
                            class="mb-2"
                    >
                        <b-card-text>
                            <h6>Reward Name</h6>
                            <p>
                                Some quick example text to build on the card title and make up the bulk of the card's content.
                                Some quick example text to build on the card title and make up the bulk of the card's content.
                            </p>
                        </b-card-text>
                        <b-button href="#" variant="primary">Pledge</b-button>
                    </b-card>
                </b-col>
            </b-row>
        </b-container>
    </div>
</template>

<script>
    export default {
        name: "Project"
    }
</script>

<style scoped>
    .nav-bar {
        margin: 20px 0 20px 0;
    }
</style>