<template>
    <!-- My Projects -->
    <section class="pb-5" id="projects">
        <h1 class="mt-5 mb-5 pb-4 text-center">My Projects</h1>

        <!-- Create a div that will contain the card deck (2 cards in a row) -->
        <!-- We will group our cards into 3 inside chunkedProjects -->
        <!-- This will loop through each grouped projects (1 grouped project contains 3 cards) -->
        <div v-for="(group, index) in chunkedProjects" :key="index" class="card-deck my-5 justify-content-center">
            <!-- We will display the individua card from the chunkedProjects -->
            <!--  This will loop through each individual project cards inside the grouped projects-->
            <ProjectCard v-for="project in group" :key="project.id" :project="project" />
        </div>

    </section>
</template>

<script setup>
    // computed method from vue is used to define reactive derived state
    import { computed } from 'vue';
    import ProjectCard from './ProjectCard.vue';
    import projects from '../data/projects.json';

    // Define the number of project cards to be displayed per row
    const chunkSize = 3;

    // Function to group projects into 3
    const chunkedProjects = computed(() => {
        // Each grouped project will be saved in chunks
        const chunks = [];

        // Loop through the projects.json in multiple of 3
        for(let i = 0; i < projects.length; i += chunkSize) {
            // slice/retrieve the 3 projects data and save it in the varibale chunks
            chunks.push(projects.slice(i, i + chunkSize));
        }

        return chunks;
    })
</script>