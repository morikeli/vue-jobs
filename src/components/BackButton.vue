<script setup>
import { RouterLink } from 'vue-router';
</script>
<template>
    <section>
        <div class="container py-3 px-3">
            <RouterLink to="/jobs" class="text-success d-flex align-items-center text-decoration-none">
            <i class="pi pi-arrow-circle-left me-3"></i> Back to Job Listings
            </RouterLink>
        </div>
    </section>
</template>
