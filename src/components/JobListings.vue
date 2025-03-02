<script setup>
import JobListing from './JobListing.vue'
import jobData from '../jobs.json'
import { ref, defineProps } from 'vue'
defineProps({
    limit: Number,
    showButton: {
        type: Boolean,
        default: false,
    },
})

const jobs = ref(jobData)
    
</script>
<template>
    <section class="bg-light min-vh-100 mb-4 d-flex align-items-center">
        <div class="container">
            <h2 class="fs-2 fw-bold text-success text-center mb-4">
                Browse jobs
            </h2>
            <div class="row g-4">
                <JobListing v-for="job in jobs.slice(0, limit || jobs.length)" :key="job.id" :job="job" />
            </div>
        </div>
    </section>

    <section v-if="showButton" class="text-center my-5">
        <a href="/jobs" class="btn btn-dark btn-lg">View All Jobs</a>
    </section>
</template>
