<template>
    <div>
        <b-card-group columns v-for="(project, index) in backedProjects" :key="index">
            <b-card
                    title="Card title that wraps to a new line"
                    img-alt="Image"
                    img-top
                    img-src="https://unsplash.com/photos/B1KFwtFFZl8"
            >
                <b-card-text>
                    <h3>{{project.project_name}}</h3>
                    <p>{{project.project_description}}</p>
                </b-card-text>
            </b-card>
        </b-card-group>
    </div>
</template>

<script>
    export default {
        name: "ProjectsBackedSection",
        props: {
            backedProjects: Array
        }
    }
</script>

<style scoped>
</style>