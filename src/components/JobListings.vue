<script setup>
import JobListing from './JobListing.vue'
import { defineProps, onMounted, reactive } from 'vue'
import { RouterLink } from 'vue-router'
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'
import axios from 'axios'

defineProps({
    limit: Number,
    showButton: {
        type: Boolean,
        default: false,
    },
})

const state = reactive({
    jobs: [],
    isLoading: true,
})

onMounted(async () => {
    try {
        const response = await axios.get('/api/jobs')
        state.jobs = response.data
    } catch (err) {
        console.error('Error fetching jobs', err)
    } finally {
        state.isLoading = false;
    }
})
</script>
<template>
    <section class="bg-light min-vh-100 my-4 d-flex align-items-center">
        <div class="container">
            <h2 class="fs-2 fw-bold text-success text-center mb-4">
                Browse jobs
            </h2>
            <!-- Loading spinner -->
            <div v-if="state.isLoading" class="text-center text-secondary py-6">
                <PulseLoader/>
            </div>

            <!-- Show job listing when the page has been loaded -->
            <div v-else class="row g-4">
                <JobListing v-for="job in state.jobs.slice(0, limit || state.jobs.length)" :key="job.id" :job="job" />
            </div>
        </div>
    </section>

    <section v-if="showButton" class="text-center my-5">
        <RouterLink to="/jobs" class="btn btn-dark btn-lg">View All Jobs</RouterLink>
    </section>
</template>
