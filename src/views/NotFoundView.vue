<script setup>
import { RouterLink } from 'vue-router'
</script>

<template>
   <section class="d-flex flex-column justify-content-center align-items-center text-center vh-100">
        <i class="pi pi-exclamation-triangle text-warning display-3 mb-4"></i>
        <h1 class="display-1 fw-bold mb-4">404 Not Found</h1>
        <p class="fs-4 mb-5">This page does not exist</p>
        <RouterLink to="/" class="btn btn-success px-4 py-2">Go Back</RouterLink>
    </section>
</template>
