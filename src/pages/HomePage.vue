<script>
    import axios from '../axios';

    export default {
        name: 'HomePage',
        data() {
            return {
                projects: [],
            };
        },
        mounted() {
            this.fetchProjects();
        },
        methods: {
            async fetchProjects() {
                try {
                    const response = await axios.get('/projects');
                    this.projects = response.data.results;
                } catch (error) {
                    console.error('Errore nel recupero dei progetti:', error);
                }
            },
        },
    };
</script>

<template>
    <div class="home-page">
        <h1>Progetti</h1>
        <ul>
            <li v-for="project in projects" :key="project.id">
                <router-link :to="{ name: 'project', params: { id: project.id } }">
                    {{ project.title }}
                </router-link>
            </li>
        </ul>
    </div>
</template>

<style scoped>
    .home-page {
        padding: 20px;
    }

    ul {
        list-style: none;
        padding: 0;
    }

    li {
        margin: 10px 0;
    }

    a {
        text-decoration: none;
        color: #3498db;
    }

    a:hover {
        color: #2980b9;
    }
</style>
