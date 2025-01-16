<script>
    import axios from '../axios';

    export default {
        name: 'ProjectPage',
        data() {
            return {
                project: null,
                error: null,
            };
        },
        mounted() {
            this.fetchProject();
        },
        methods: {
            async fetchProject() {
                try {
                    const response = await axios.get(`/projects/${this.$route.params.id}`);
                    this.project = response.data.result;
                } catch (error) {
                    console.error('Errore nel recupero del progetto:', error);
                    this.error = 'Progetto non trovato.';
                }
            },
        },
    };
</script>

<template>
    <div class="project-page">
        <div v-if="error" class="error">
            <p>{{ error }}</p>
        </div>
        <div v-else-if="project">
            <h1>{{ project.title }}</h1>
            <p>{{ project.description }}</p>
            <p>
                <strong>Repository:</strong>
                <a :href="project.repo_url" target="_blank">{{ project.repo_url }}</a>
            </p>
        </div>
        <div v-else>
            <p>Caricamento...</p>
        </div>
    </div>
</template>

<style scoped>
    .project-page {
        padding: 20px;
    }

    .error {
        color: red;
        font-weight: bold;
    }
</style>
