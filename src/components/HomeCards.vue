<script setup>
import Card from '@/components/Card.vue'
import { RouterLink } from 'vue-router'
</script>
<template>
    <section class="py-4">
        <div class="container">
            <div class="row g-4">
                <div class="col-md-6">
                    <Card>
                        <h2 class="h4 fw-bold">For Developers</h2>
                        <p class="mt-2 mb-4">Browse our Vue jobs and start your career today</p>
                        <RouterLink to="jobs.html" class="btn btn-dark">Browse Jobs</RouterLink>
                    </Card>
                </div>
                <div class="col-md-6">
                    <Card bg="bg-success bg-opacity-25">
                        <h2 class="h4 fw-bold">For Employers</h2>
                        <p class="mt-2 mb-4">List your job to find the perfect developer for the role</p>
                        <RouterLink to="/jobs/add" class="btn btn-success">Add Job</RouterLink>
                    </Card>
                </div>
            </div>
        </div>
    </section>
</template>
